pipeline {
    agent any

    environment {
        IMAGE_NAME = 'my-docker-imagezxcv'
        CONTAINER_NAME = 'my-containerzxcv'
        PORT_MAPPING = '8083:5901'
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
                    sh "docker build -t ${env.IMAGE_NAME} ."
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    echo 'Running Docker container...'

                    // Use different commands based on the operating system
                    if (isUnix()) {
                        sh "docker run -d -p ${env.PORT_MAPPING} --name ${env.CONTAINER_NAME} ${env.IMAGE_NAME}"
                    } else {
                        bat "docker run -d -p ${env.PORT_MAPPING} --name ${env.CONTAINER_NAME} ${env.IMAGE_NAME}"
                    }
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
                    sh "docker stop ${env.CONTAINER_NAME} || true"
                    sh "docker rm ${env.CONTAINER_NAME} || true"
                }
            }
        }
    }
}
