pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/OP-CODER/hiring-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Check if Buildx is supported
                    sh 'docker buildx version'  // Check if Buildx is installed
                    sh 'docker buildx create --use' // Enable Buildx if needed
                    sh 'docker buildx build --tag hiring-app:latest .'
                }
            }
        }

        stage('Push to DockerHub') {
            environment {
                DOCKERHUB_CREDENTIALS = credentials('docker')  // 'docker' is the credential ID
            }
            steps {
                script {
                    // Login to DockerHub using Jenkins credentials
                    sh """
                        echo \$DOCKERHUB_CREDENTIALS_PSW | docker login -u \$DOCKERHUB_CREDENTIALS_USR --password-stdin
                        docker tag hiring-app:latest anas974/hiring-app:latest
                        docker push anas974/hiring-app:latest
                    """
                }
            }
        }
    }
}
