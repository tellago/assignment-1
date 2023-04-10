pipeline {
    agent any
    stages {
        stage('checkout') {
            steps {
              git 'https://github.com/tellago/assignment-1.git'
              }
        }
        stage('docker build') {
            steps {
                sh "docker build  -t foodapp:v1 ."
            }
        }
        stage('creating docker container') {
            steps {
                sh "docker run -dt -p 8082:8080 foodapp:v1"
            }
        }
        stage('Login to dockerhub') {
          steps {
              withCredentials([usernamePassword(credentialsId: 'dockerhub_creds', passwordVariable: 'dockerhub_password', usernameVariable: 'dockerhub_username')]) {
                  
            sh 'docker login -u $dockerhub_username -p $dockerhub_password'
            }
          }
          }
        stage('Pushing Image to Dockerhub') {
            steps {
                sh 'docker tag foodapp:v1 saikrishna21/foodapp-tomact:v1'
                sh 'docker push saikrishna21/foodapp-tomact:v1'
            }
        }
      
        stage ('CleanUP') {
         steps {
             cleanWs() 
        }
    }
  }
}
