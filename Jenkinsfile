pipeline {
    agent { label 'jenkins-agent'}
    tools {
        jdk 'Java17'
        maven 'Maven3'
    } 

    environment {
	    APP_NAME = "register-app-pipeline"
            RELEASE = "1.0.0"
            DOCKER_USER = "shashankpatil82"
            DOCKER_PASS = 'dockerhub'
            IMAGE_NAME = "${DOCKER_USER}" + "/" + "${APP_NAME}"
            IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
	    JENKINS_API_TOKEN = credentials("JENKINS_API_TOKEN")
    }
    stages{
        stage("Cleanup workspace") {
            steps {
                cleanWs()
            }
            }
        stage("Checkout from SCM")  {
            steps {
              git branch: 'main', credentialsId: 'github', url: 'https://github.com/Shashankp82/register-app.git'
            }
        }
        stage("Build Application")  {
            steps {
                sh "mvn clean package"
            }
        }
        stage("Application Testing")  {
            steps {
                sh "mvn test"
            }  
        }
	stage("Build and Push Docker image")  {
            steps {
                script {
                    docker.withRegistry('',DOCKER_PASS) {
                        docker_image = docker.build "${IMAGE_NAME}"
                    }

                    docker.withRegistry('',DOCKER_PASS) {
                        docker_image.push("${IMAGE_TAG}")
                        docker_image.push('latest')
                    }
                }
             }  
         }    
         
     }
  
 }


