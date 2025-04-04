pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'saitejabatti/devops-static-site'
        DOCKER_CREDENTIALS_ID = 'docker-hub-creds' // Jenkins credentials ID
        EC2_USER = 'ubuntu'
        EC2_HOST = '3.86.166.2'
        SSH_KEY_ID = 'ec2-ssh-key' // Jenkins credentials ID for SSH private key
    }

    stages {

        stage('Clone Repository') {
            steps {
                echo "Cloning repository..."
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker image..."
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                echo "Pushing image to Docker Hub..."
                withCredentials([usernamePassword(credentialsId: "${DOCKER_CREDENTIALS_ID}", usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh """
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker push $DOCKER_IMAGE
                    """
                }
            }
        }

        stage('Deploy on EC2') {
            steps {
                echo "Deploying to EC2..."
                sshagent([SSH_KEY_ID]) {
                    sh """
                        ssh -o StrictHostKeyChecking=no ubuntu@35.169.106.63 '
                            docker pull $DOCKER_IMAGE
                            docker stop devops-site || true && docker rm devops-site || true
                            docker run -d -p 80:80 --name devops-site $DOCKER_IMAGE
                        '
                    """
                }
            }
        }
    }
}
