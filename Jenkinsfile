pipeline {
    agent any

    tools {
        // Make sure 'Maven' matches the name configured in your Jenkins tools
        maven 'Maven' 
    }

    environment {
        // Using the credentials ID for Docker Hub that you've configured in Jenkins
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials-id')
        IMAGE_TAG = 'anjalisingh99/banking:latest'
    }

    stages {
        stage('Checkout') {
            steps {
                // Git checkout
                git 'https://github.com/Anjali-Singh-99/star-agile-banking-finance.git'
            }
        }

        stage('Build') {
            steps {
                // Maven build
                sh 'mvn clean install'
            }
        }

        stage('Docker Build and Push') {
            steps {
                script {
                    // Docker build and push
                    docker.withRegistry('https://registry.hub.docker.com', DOCKERHUB_CREDENTIALS) {
                        def customImage = docker.build(IMAGE_TAG)
                        customImage.push()
                    }
                }
            }
        }
    }

    post {
        always {
            // This is a post-build step, you can add actions to perform after the pipeline runs
            echo 'The pipeline is complete.'
        }
    }
}
