pipeline {
    agent any

    environment {
      DOCKERHUB_CREDENTIALS='doc_cred_c2'
      IMAGE_NAME = 'sandhyag4/new_docker_image'
      }

    stages {

        stage('Build java application') {
            steps {
                bat 'javac HelloWorld.java'
            }
        }
      stage('Run java program') {
            steps {
                bat 'java HelloWorld'
            }
        }

      stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME%:latest .'
            }
        }
   


        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'doc_cred_c2',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    bat 'echo %PASS%| docker login -u %USER% --password-stdin'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                bat 'docker push %IMAGE_NAME%:latest'
            }
        }
    }
}
