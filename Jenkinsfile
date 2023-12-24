pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials-id')
        IMAGE_TAG = 'anjalisingh99/banking:latest'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Anjali-Singh-99/star-agile-banking-finance.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Docker Build and Push') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', DOCKERHUB_CREDENTIALS) {
                        def customImage = docker.build(IMAGE_TAG)
                        customImage.push()
                    }
                }
            }
        }
    }
}
