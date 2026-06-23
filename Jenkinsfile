pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Build') {
      steps {
        echo 'CloudBees CI demo — build successful'
        sh 'ls -la'
      }
    }
  }
}
