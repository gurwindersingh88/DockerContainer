pipeline {
    agent any

    environment {
        IMAGE_NAME = 'my-docker-imagezxc'
        CONTAINER_NAME = 'my-containerzxc'
        PORT_MAPPING = '8080:5901'
    }

    stages {
        stage('Checkout') {
            steps {
                // Check out your code repository
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image
                    echo 'Building Docker image...'
                    sh "docker build -t ${env.IMAGE_NAME} ."
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Run Docker container
                    echo 'Running Docker container...'
                    if (isUnix()) {
                        sh "nohup docker run -d -p ${env.PORT_MAPPING} --name ${env.CONTAINER_NAME} ${env.IMAGE_NAME} &"
                    } else {
                        sh "start /B docker run -d -p ${env.PORT_MAPPING} --name ${env.CONTAINER_NAME} ${env.IMAGE_NAME}"
                    }
                }
            }
        }

        stage('Post-Deployment') {
            steps {
                echo 'Performing post-deployment steps...'
                // Add post-deployment steps if needed
            }
        }

        stage('Cleanup') {
            steps {
                script {
                    // Clean up: Stop and remove the Docker container
                    echo 'Cleaning up...'
                    sh "docker stop ${env.CONTAINER_NAME} || true"
                    sh "docker rm ${env.CONTAINER_NAME} || true"
                }
            }
        }
    }
}
