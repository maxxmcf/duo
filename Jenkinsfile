pipeline {
    agent any
    stages {
        stage('welcome jenky') {
            steps {
                sh '''
                echo "hi there - welcome to the pipeline"
                '''
            }
        }
        stage('buildy dockery images') {
            steps {
                sh '''
                docker build -t maxmcf13/appkub:latest -t maxmcf13/appkub:v$BUILD_NUMBER .
                '''
            }
        }
        stage('pushy dockery images') {
            steps {
                sh '''
                docker push maxmcf13/appkub:latest
                docker push maxmcf13/appkub:v$BUILD_NUMBER
                '''
            }
        }
        stage('rolling rolling restart') {
            steps {
                sh '''
                kubectl apply -f ./k8s-deployments -n prod
                kubectl rollout restart deployment flask-deployment -n prod
                '''
            }
        }
        stage('tidy space tidy mind') {
            steps {
                sh '''
                docker rmi maxmcf13/appkub:latest
                docker rmi maxmcf13/appkub:v$BUILD_NUMBER

                docker system prune -a --force
                '''
            }
        }
    }
}
