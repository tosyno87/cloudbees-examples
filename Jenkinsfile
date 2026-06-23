pipeline {
  agent {
    kubernetes {
      yaml """
apiVersion: v1
kind: Pod
spec:
  serviceAccountName: jenkins-agents
  containers:
  - name: jnlp
    image: cloudbees/cloudbees-core-agent:2.555.3.36983
    tty: true
    resources:
      requests:
        memory: 512Mi
        cpu: 250m
      limits:
        memory: 1Gi
        cpu: 500m
"""
    }
  }

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
