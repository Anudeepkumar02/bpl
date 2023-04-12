pipeline {
    agent any

    stages {
        stage('SCM') {
            steps {
                git 'https://github.com/Anudeepkumar02/bpl.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('artifact download') {
            steps {
                sh 'aws s3 cp target/*.war s3://warfileswebproject/bpl/bpl.war'
                sh 'aws s3 cp target/*.war s3://warfileswebproject/bpl/bpl$BUILD_NUMBER.war'
            }
        }
        stage('Build docker image') {
            steps {
                script{
                    sh 'docker build -t 2222s/sonyimages .'
                }
            }
        }
        stage('pushing docker image to docker hub') {
            steps {
                script{
                    withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u 2222s -p ${dockerhubpwd}'        
                        
    
}
                    sh 'docker push 2222s/sonyimages:latest'
                
                }
            }
        }
        
    }
}
