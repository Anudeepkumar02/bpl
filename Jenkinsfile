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
                script {
                    docker build -t 2222s/fristimage .
                }
            }
        }
    }
}
