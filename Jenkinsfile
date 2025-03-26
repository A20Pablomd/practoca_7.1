pipeline {
  environment {
    IMAGEN = "a20pablomd/Amellor"
    BUILD_NUMBER = "1"
    USUARIO = 'USER_DOCKERHUB'
  }
  agent any
  stages {
    stage('Clone') {
      steps {
        git branch: "main", url: 'https://github.com/A20Pablomd/practoca_7.1'
      }
    }
    stage('Build') {
      steps {
        script {
          newApp = docker.build "$IMAGEN:$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy') {
      steps {
        script {
          docker.withRegistry( '', USUARIO ) {
            newApp.push()
          }
        }
      }
    }
    stage('Clean Up') {
      steps {
        sh "docker rmi $IMAGEN:$BUILD_NUMBER"
        }
     }
   }
}
