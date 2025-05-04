pipeline {
    agent any

    environment {
        EC2_USER = 'ec2-user'
        EC2_HOST = '18.206.224.153'  // Replace with Elastic IP
        EC2_KEY = '/var/lib/jenkins/awslogin.pem'
' // Jenkins server path to .pem
        TARGET_DIR = '/var/www/html'      // Example: Apache web root
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Saitejabatti/devops-static-site.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the static website...'
                // For static HTML sites, this may be minimal or empty
            }
        }

        stage('Deploy to EC2') {
            steps {
                echo "Deploying to EC2 instance..."
                sh """
                chmod 400 ${EC2_KEY}
                scp -o StrictHostKeyChecking=no -i ${EC2_KEY} -r * ${EC2_USER}@${EC2_HOST}:${TARGET_DIR}
                """
            }
        }
    }

    post {
        success {
            echo 'Deployment completed successfully.'
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}
