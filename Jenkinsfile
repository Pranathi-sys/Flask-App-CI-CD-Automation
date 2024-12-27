pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('flask-app')
                }
            }
        }

        stage('Login to AWS ECR') {
            steps {
                script {
                    sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 390844751355.dkr.ecr.us-east-1.amazonaws.com'
                }
            }
        }

        stage('Tag and Push Docker Image') {
            steps {
                script {
                    sh '''
                    docker tag flask-app:latest 390844751355.dkr.ecr.us-east-1.amazonaws.com/flask-app:latest
                    docker push 390844751355.dkr.ecr.us-east-1.amazonaws.com/flask-app:latest
                    '''
                }
            }
        }

        stage('Deploy to ECS') {
            steps {
                script {
                    sh 'aws ecs update-service --cluster flask-app-cluster --service flask-app-service --force-new-deployment'
                }
            }
        }
    }
}