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
                sh 'docker build --tag hiring-app:latest .'
            }
        }

        stage('Push to DockerHub') {
            environment {
                DOCKERHUB_CREDENTIALS = credentials('docker')  // 'docker' is the credential ID
            }
            steps {
                sh """
                    echo \$DOCKERHUB_CREDENTIALS_PSW | docker login -u \$DOCKERHUB_CREDENTIALS_USR --password-stdin
                    docker tag hiring-app:latest anas974/hiring-app:latest
                    docker push anas974/hiring-app:latest
                """
            }
        }
    }
}
