pipeline {
    agent any

    tools {
        // Make sure 'Maven' matches the name configured in your Jenkins tools
        maven 'Maven' 
    }

    environment {
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
                    // Hardcoded Docker credentials (not recommended)
                    def dockerUsername = 'anjalisingh99'
                    def dockerPassword = 'Anjali@123'
                    
                    // Docker login
                    sh "echo '${dockerPassword}' | docker login -u '${dockerUsername}' --password-stdin"

                    // Docker build and push
                    def customImage = docker.build(IMAGE_TAG)
                    customImage.push()

                    // Docker logout
                    sh 'docker logout'
                }
            }
        }
    }

    post {
        always {
            // Post-build step
            echo 'The pipeline is complete.'
        }
    }
}
