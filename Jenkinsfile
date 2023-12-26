pipeline {
    agent any

    tools {
        maven 'Maven' 
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

        stage('Deploy with Ansible') {
            steps {
                script {
                    ansiblePlaybook(
                        playbook: 'ansible-playbook.yml',
                        inventory: 'hosts.ini',
                        extras: '--private-key /root/.ssh/id_rsa' // Replace with the actual path to your private key
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
