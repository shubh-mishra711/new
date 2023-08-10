pipeline {

  environment {
    dockerimagename = "shubhmishra/weather-jenkns-app"
    dockerImage = ""
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/shubh-mishra711/new.git'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build dockerimagename
        }
      }
    }

    stage('Pushing Image') {
      environment {
               registryCredential = 'dockerhub-credentials'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push("latest")
          }
        }
      }
    }

    stage('Run Docker Container'){
      steps{
        sh ("docker run -d --name weatherapp1 -p 5000:3000 shubhmishra/weather-jenkns-app")
      }
    }


  }

}