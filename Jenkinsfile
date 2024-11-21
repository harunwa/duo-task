pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh '''
                docker build -t stratcastor/duo-jenk:latest -t stratcastor/duo-jenk:v${BUILD_NUMBER} .
                '''
            }
        }
        stage('Push') {
            steps {
                sh '''
                docker push stratcastor/duo-jenk:latest
                docker push stratcastor/duo-jenk:v${BUILD_NUMBER}
                '''
            }
        }
        stage('Deploy') {
            steps {
                sh'''
                kubectl apply -f ./kubernetes
                kubectl set image deployment/flask-deployment flask-container=stratcastor/duo-jenk:v${BUILD_NUMBER}
                '''
            }
        }
    }
}
