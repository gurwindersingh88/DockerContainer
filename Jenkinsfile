pipeline {
    agent any

    environment {
        IMAGE_NAME = 'my-docker-image'
        CONTAINER_NAME = 'my-container123456'
        PORT_MAPPING = '8086:5901'
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image
                    sh "docker build -t ${env.IMAGE_NAME} ."
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Run Docker container
                    sh "docker run -d -p ${env.PORT_MAPPING} --name ${env.CONTAINER_NAME} ${env.IMAGE_NAME}"
                }
            }
        }

        stage('Cleanup') {
            steps {
                script {
                    // Clean up: Stop and remove the Docker container
                    sh "docker stop ${env.CONTAINER_NAME} || true"
                    sh "docker rm ${env.CONTAINER_NAME} || true"
                }
            }
        }
    }
}
