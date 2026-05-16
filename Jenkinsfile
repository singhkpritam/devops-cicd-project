pipeline {
    agent any

    stages {

        stage('Build Image') {
            steps {
                sh '''
                eval $(minikube docker-env)
                docker build -t devops-project:${BUILD_NUMBER} .
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                kubectl set image deployment/frontend-deployment \
                devops-project=devops-project:${BUILD_NUMBER}

                kubectl patch deployment frontend-deployment \
                -p '{"spec":{"template":{"spec":{"containers":[{"name":"devops-project","imagePullPolicy":"Never"}]}}}}'
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
