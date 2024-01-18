pipeline {
    agent any

    environment {
        IMAGE_NAME = 'my-docker-image321'
        CONTAINER_NAME = 'my-container321'
        PORT_MAPPING = '8085:5901'
    }

    stages {
        stage('Install Docker') {
            steps {
                // Install Docker
                sh 'curl -fsSL https://get.docker.com -o get-docker.sh'
                sh 'sh get-docker.sh'
                sh 'sudo usermod -aG docker $USER'
                sh 'sudo systemctl enable docker'
                sh 'sudo systemctl start docker'
            }
        }

        stage('Run Inline Script') {
            steps {
                script {
                    // Print Docker version
                    sh 'docker --version'

                    // Echo a message
                    echo 'Hello, this is a simple inline script!'
                }
            }
        }

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

        stage('Post-Deployment') {
            steps {
                // Perform post-deployment tasks if needed
                echo 'Post-deployment tasks...'
            }
        }

        stage('Cleanup') {
            steps {
                // Clean up: Stop and remove the Docker container
                script {
                    sh "docker stop ${env.CONTAINER_NAME} || true"
                    sh "docker rm ${env.CONTAINER_NAME} || true"
                }
            }
        }
    }
}
