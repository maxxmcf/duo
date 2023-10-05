pipeline {
    agent any
    stages {
        stage('welcome') {
            steps {
                sh '''
                echo "hi there - welcome to the pipeline"
                '''
            }
        }
        stage('build docker images') {
            steps {
                sh '''
                docker build -t maxmcf13/appkub:latest ./nginx
                '''
            }
        }
        stage('push docker images') {
            steps {
                sh '''
                docker push maxmcf13/appkub:latest
                '''
            }
        }
        stage('rolling rolling restart') {
            steps {
                sh 'kubectl rollout restart deployment flask-deployment'
            }
        }
    }
}
