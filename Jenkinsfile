pipeline {
    agent any

    environment {
        IMAGE_NAME = "devops-project"
        IMAGE_TAG = "${BUILD_NUMBER}"
    }

    stages {

        stage('Clone Code') {
            steps {
                git url: 'https://github.com/singhkpritam/devops-cicd-project.git', branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t devops-project:$BUILD_NUMBER .
                '''
            }
        }

        stage('Deploy To Kubernetes') {
            steps {
                sh '''
                kubectl set image deployment/frontend-deployment frontend-container=$IMAGE_NAME:$IMAGE_TAG
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh '''
                kubectl rollout status deployment/frontend-deployment
                '''
            }
        }
    }
}
