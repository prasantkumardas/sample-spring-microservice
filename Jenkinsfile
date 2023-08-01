pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t prasantdas123/docker-hub .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
        echo 'Login completed'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push prasantdas123/docker-hub'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
