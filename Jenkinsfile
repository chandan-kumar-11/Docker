pipeline {
    environment {
    registry = "chandankumar10942/docker-repo"
    registryCredential = 'dockerhub'
    dockerImage = ''
    }
    agent any

    stages {
        stage('Checkout') {
               steps {
                   git branch: 'main', 'url': 'https://github.com/chandan-kumar-11/Docker.git'
               }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    def dockerImageTag = "my-app-image:${env.BUILD_NUMBER}"
                    sh "docker build -t ${dockerImageTag} ."
                }
            }
        }

        stage('Create Docker Container') {
            steps {
                script {
                    def dockerContainerName = "my-app-container-${env.BUILD_NUMBER}"
                    sh "docker run -d --name ${dockerContainerName} my-app-image:${env.BUILD_NUMBER}"
                }
            }
        }
         stage('pull image from Docker Hub') {
           steps {
              sh "docker pull chandankumar10942/myapp:v1"
            } 
            
                  
           
        }

        stage('Publish image to Docker Hub') {
           steps {
              script{
                   withDockerRegistry([ credentialsId: "dockerhub", url: "" ]) {
                    sh  " docker push my-app-image:${env.BUILD_NUMBER}"
                  }
              }  
            } 
            
                  
           
        }
    
    }
        
       
}