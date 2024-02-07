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
	   }    
        }	 
     
  


