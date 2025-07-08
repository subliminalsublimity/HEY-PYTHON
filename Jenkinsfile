pipeline {
    agent any 
    environment {
        DOCKERHUB_CREDENTIALS = credentials('DockerHubCredentials')
    }
    stages {
        stage('SCM Checkout'){
            steps {
                git 'https://github.com/subliminalsublimity/HEY-PYTHON.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                docker build -t  python2:$BUILD_NUMBER .
            }
        }

        stage('Login to DockerHub') {
            steps {
                'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Push Docker Image') {
            steps {
                'docker push python2:$BUILD_NUMBER'
            }
        }
        
    }
}
