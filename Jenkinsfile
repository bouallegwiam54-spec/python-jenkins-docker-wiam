pipeline {
    agent any

    environment {
        IMAGE_NAME = "python-print-app:latest"
    }

    stages {

        stage('Checkout') {
            steps {
                // Récupérer le code depuis GitHub (correct repository)
                git branch: 'main', url: 'https://github.com/bouallegwiam54-spec/python-jenkins-docker-wiam.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo "Building Docker image ${IMAGE_NAME}..."
                    docker.build("${IMAGE_NAME}")
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    echo "Stopping old container if exists..."
                    sh 'docker rm -f python-print-app || true'
                    
                    echo "Running new container..."
                    sh 'docker run --name python-print-app ${IMAGE_NAME}'
                }
            }
        }

    }

    post {
        success {
            echo 'Pipeline terminé avec succès !'
        }
        failure {
            echo 'Pipeline échoué.'
        }
    }
}
