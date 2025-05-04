pipeline {
    agent any

    environment {
        PEM_PATH = 'C:/Users/ASUS/Downloads/awslogin.pem' // Local path to your .pem file
        EC2_IP = '18.206.224.153'
        SSH_USER = 'ubuntu'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/Saitejabatti/devops-static-site.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the static website...'
                // If any build command needed, add here (like npm build)
            }
        }

        stage('Deploy to EC2') {
            steps {
                echo 'Deploying to EC2 instance...'
                // Replace index.html path as needed
                sh """
                    scp -i "$PEM_PATH" -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null index.html $SSH_USER@$EC2_IP:/var/www/html/
                """
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}
