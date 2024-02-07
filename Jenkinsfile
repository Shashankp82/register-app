pipeline {
    agent { label 'jenkins-agent'}
    tools {
        jdk 'Java17'
        maven 'Maven3'
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


