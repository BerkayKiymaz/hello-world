pipeline {

  agent any

  environment {
    DOCKERHUB_CREDENTIALS=credentials('dockerhub') 
  }

  stages {

    stage("Git Checkout") {
      steps {
        script {
           sh "git clone https://github.com/BerkayKiymaz/hello-world.git"
        }
      }
    }

    stage("Maven Build") {
      steps {
        script {
          sh "mvn compile"
          sh "echo Maven compile has completed!"
        }
      }
    }
    
    stage("Maven Test") {
      steps {
        script {
          sh "mvn test"
          sh "echo Maven test has completed!"
        }
      }
    }
    
    stage("Maven Package") {
      steps {
        script {
          sh "mvn package"
          sh "echo Maven package has completed!"
        }
      }
    }
    
  
    stage("Build & Push Docker Image") {
      steps {
        script {
          sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
          sh "docker build -t bkiymaz/helloworld ."
          sh "docker push bkiymaz/helloworld"
        }
      }
    } 
  }
}
