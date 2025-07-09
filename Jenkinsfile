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
                script {
              sh "docker build -t python2 ."
                }
            }
        }

        stage('Login to DockerHub') {
            steps {
                script{
               sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u "$DOCKERHUB_CREDENTIALS_USR --password-stdin'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                sh "docker tag python2 dakshgaur10/hey-python-flask:v1.0"
                sh "docker push dakshgaur10/hey-python-flask:v1.0"

            }
        }
    }

    stage('Run Docker Container'){
        steps {
            script {
                sh 'docker rm python2-container --force || true'
                sh "docker run --name python2-container -p 8085:80 -d python2"
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
