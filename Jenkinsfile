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
                    // Docker build and push with credentials
                    withCredentials([usernameColonPassword(credentialsId: 'dockerhub', variable: 'docker_creds')]) {
                        docker.withRegistry('https://registry.hub.docker.com', docker_creds) {
                            def customImage = docker.build(IMAGE_TAG)
                            customImage.push()
                        }
                    }
                }
            }
        }
    }

    post {
        always {
            // This is a post-build step
            echo 'The pipeline is complete.'
        }
    }
}
