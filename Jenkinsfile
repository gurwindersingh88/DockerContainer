pipeline {
    agent any

    environment {
        IMAGE_NAME = 'my-docker-imagezxcvbn'
        CONTAINER_NAME = 'my-containerzxcvbn'
        PORT_MAPPING = '8085:5901'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo 'Building Docker image...'
                    bat "docker build -t ${env.IMAGE_NAME} ."
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    echo 'Running Docker container...'
                    bat "docker run -d -p ${env.PORT_MAPPING} --name ${env.CONTAINER_NAME} ${env.IMAGE_NAME}"
                }
            }
        }

        stage('Post-Deployment') {
            steps {
                echo 'Performing post-deployment steps...'
            }
        }

        stage('Cleanup') {
            steps {
                script {
                    echo 'Cleaning up...'
                    bat "docker stop ${env.CONTAINER_NAME} || true"
                    bat "docker rm ${env.CONTAINER_NAME} || true"
                }
            }
        }
    }
}
