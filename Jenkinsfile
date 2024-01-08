pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dh_cred')
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Init') {
            steps {
                sh 'echo Init Step'
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }

        

        stage('Build proj') {
            
            steps {
                dir('client') {
                    sh 'sudo docker build -t $DOCKERHUB_CREDENTIALS_USR/client:$BUILD_ID .'
                    sh 'sudo docker push $DOCKERHUB_CREDENTIALS_USR/client:$BUILD_ID'
                    sh 'sudo docker rmi $DOCKERHUB_CREDENTIALS_USR/client:$BUILD_ID'
                }
            }
        }

        stage('logout') {
            steps {
                sh 'sudo docker logout'
            }
        }
    }
}