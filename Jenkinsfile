pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('Docker')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t saiprabhudarla/jenkins_cicd_repo .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push saiprabhudarla/jenkins_cicd_repo'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
