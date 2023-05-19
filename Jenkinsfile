pipeline {
    agent {label 'docker-build-node'}
    environment {
    DOCKERHUB_CREDENTIALS = credentials('docker-jenkins')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/srikanth0537/nodejs-demo.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t nukalasrikanth/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push nukalasrikanth/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

