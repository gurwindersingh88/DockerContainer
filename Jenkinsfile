pipeline {
    agent any

    environment {
        IMAGE_NAME = 'my-docker-image009988'
        CONTAINER_NAME = 'my-container009988'
        PORT_MAPPING = '8083:5901'
    }

    stages {
        stage('Install Docker') {
            steps {
                // Install Docker using the Docker tool
                tool name: 'Docker', type: 'org.jenkinsci.plugins.docker.commons.tools.DockerTool'
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
                    docker.build(env.IMAGE_NAME, '.')
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Run Docker container
                    def container = docker.image(env.IMAGE_NAME).run("-p ${env.PORT_MAPPING} --name ${env.CONTAINER_NAME} -d")
                    def containerId = container.id
                    echo "Docker container ID: ${containerId}"
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
