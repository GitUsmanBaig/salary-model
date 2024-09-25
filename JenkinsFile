pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker-hub-credentials')
    }
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Building the Docker image and tagging it with the build ID
                    docker.build("i211132usman/your_dockerhub_repo:${env.BUILD_ID}")
                }
            }
        }
        stage('Push Image to Docker Hub') {
            steps {
                script {
                    // Logging into Docker Hub and pushing the image
                    docker.withRegistry('https://index.docker.io/v1/', 'DOCKERHUB_CREDENTIALS') {
                        docker.image("i211132usman/your_dockerhub_repo:${env.BUILD_ID}").push()
                    }
                }
            }
        }
    }
    post {
        always {
            // Cleaning up the Docker images to save space on the Jenkins server
            echo 'Cleaning up...'
            sh "docker rmi i211132usman/your_dockerhub_repo:${env.BUILD_ID}"
        }
    }
}