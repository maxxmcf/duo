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
                docker build -t maxmcf13/nginxkub:latest ./flask-app
                '''
            }
        }
        stage('push docker images') {
            steps {
                sh '''
                docker push maxmcf13/appkub:latest
                docker push maxmcf13/nginxkub:latest
                '''
            }
        }
        stage('rolling rolling restart') {
            steps {
                //
            }
        }
    }
}
