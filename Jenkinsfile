pipeline {
    agent any
    environment {
        DOCKER_USERNAME = credentials('docker-username') 
        DOCKER_PASSWORD = credentials('docker-password') 
    }
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t i211132usman/salary-predictor-usingjenkins:${env.BUILD_ID} ."
                }
            }
        }
        stage('Push Image to Docker-Hub') {
            steps {
                script {
                    sh 'echo $DOCKER_PASSWORD | docker login --username $DOCKER_USERNAME --password-stdin'
                    sh "docker push i211132usman/salary-predictor-usingjenkins:${env.BUILD_ID}"
                }
            }
        }
    }
    post {
        always {
            echo 'Cleaning'
            sh "docker rmi i211132usman/salary-predictor-usingjenkins:${env.BUILD_ID}"
        }
    }
}
