pipeline {
    agent any 
    environment {
        DOCKERHUB_CREDENTIALS = credentials('DockerHubCredentials')
        IMAGE_NAME = 'dakshgaur10/hey-python-flask'
    }

    stages {
        stage('SCM Checkout'){
            steps {
                git branch: 'main' , url:'https://github.com/subliminalsublimity/HEY-PYTHON.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
              sh "docker build -t ${IMAGE_NAME}:$BUILD_NUMBER ."
                }
            }
        }

        stage('Login to DockerHub') {
            steps {
                script{
               sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u "$DOCKERHUB_CREDENTIALS_USR" --password-stdin'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                sh "docker push ${IMAGE_NAME}:${BUILD_NUMBER}"
            }
        }
    }

    stage('Run Docker Container'){
        steps {
            script {
                sh 'docker rm python2-container --force || true'
                sh "docker run --name python2-container -p 8085:80 -d ${IMAGE_NAME}:${BUILD_NUMBER}"
            }
        }
    }
}


post {
    always {
        script {
            sh 'docker logout'
        }
    }
}
}
