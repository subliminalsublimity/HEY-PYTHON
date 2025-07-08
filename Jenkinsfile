pipeline {
    agent any

   environment { 
       DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
   }

   stages { 
       stage('SCM Checkout') {
           steps {
               git branch: 'main', url: 'https://github.com/subliminalsublimity/HEY-PYTHON.git'
           
           }
       }
    

       stage('Docker Login') {
           steps {
               echo 'Logon in to docker hub'
               sh 'echo dckr_pat_v320MseFjoYH-IXHnwyEOV7OBBc | docker login -u dakshgaur10 --password-stdin docker.io'
               echo 'Login Successfull'
           }
       }



        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("your-docker-registry/your-image-name:${env.BUILD_NUMBER}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry(' https://registry.hub.docker.com', 'dakshgaur10') {
                        dockerImage.push()
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Docker image built and pushed successfully!'
        }
    }
}