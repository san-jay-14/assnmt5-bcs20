pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "sanjay1410/2023bcs0020"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/san-jay-14/assnmt5-bcs20.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %DOCKER_IMAGE% .'
            }
        }

        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    bat 'echo %PASS% | docker login -u %USER% --password-stdin'
                }
            }
        }
        
        stage('Push Image') {
            steps {
                bat 'docker push %DOCKER_IMAGE%'
            }
        }
    }
}
