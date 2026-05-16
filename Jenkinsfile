pipeline {
    agent any

    stages {

        stage('Build Image') {
            steps {
                sh 'docker build -t devops-project:${BUILD_NUMBER} .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                kubectl set image deployment/frontend-deployment \
                devops-project=devops-project:${BUILD_NUMBER}
                '''
            }
        }

        stage('Verify') {
            steps {
                sh 'kubectl rollout status deployment/frontend-deployment'
            }
        }
    }
}
