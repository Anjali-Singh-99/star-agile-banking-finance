pipeline {
    agent any

    tools {
        maven 'Maven'
        // Ensure that Ansible is configured in your Jenkins tools
        ansible 'Ansible'
    }

    environment {
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
                    def dockerUsername = 'anjalisingh99'
                    def dockerPassword = 'Anjali@123'
                    
                    sh "echo '${dockerPassword}' | docker login -u '${dockerUsername}' --password-stdin"
                    def customImage = docker.build(IMAGE_TAG)
                    customImage.push()
                }
            }
        }

        // New stage for Ansible deployment
        stage('Deploy with Ansible') {
            steps {
                script {
                    // Running the Ansible playbook
                    ansiblePlaybook(
                        playbook: 'ansible_playbook.yaml',
                        inventory: 'hosts.ini',
                        
                    )
                }
            }
        }
    }

    post {
        always {
            echo 'The pipeline is complete.'
        }
    }
}
