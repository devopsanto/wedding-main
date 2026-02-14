pipeline {
    agent any

    environment {
        EC2_HOST = "13.200.40.76"
        EC2_USER = "ubuntu"
    }

    stages {

        stage('Deploy Nginx to EC2') {
            steps {
                script {
                    sh """
                    ssh -o StrictHostKeyChecking=no ${EC2_USER}@${EC2_HOST} '
                        docker rm -f nginx-server || true
                        docker pull nginx:latest
                        docker run -d --name nginx-server -p 80:80 nginx:latest
                    '
                    """
                }
            }
        }
    }

    post {
        success {
            echo "✅ Nginx deployed successfully!"
        }
        failure {
            echo "❌ Deployment failed!"
        }
    }
}
