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
  - name: kubectl
    image: registry.k8s.io/kubectl:v1.34.0
    command: ["sleep"]
    args: ["infinity"]
    tty: true
    resources:
      requests:
        memory: 128Mi
        cpu: 100m
      limits:
        memory: 256Mi
        cpu: 250m
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
    stage('Deploy') {
      steps {
        container('kubectl') {
          sh 'kubectl apply -f k8s/deployment.yaml -n demo-app'
          sh 'kubectl rollout status deployment/hello -n demo-app --timeout=120s'
          sh 'kubectl get pods,svc -n demo-app'
        }
      }
    }
  }
}
