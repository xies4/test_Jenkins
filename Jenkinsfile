pipeline {
  agent any
  triggers {
        // Poll SCM every 5 minutes
        pollSCM('H/5 * * * *') 
    }
  stages {
    stage('TEST') {
      steps {
        echo 'Jenkinsfile is running'
        sh 'pwd'
        sh 'git rev-parse --short HEAD'
        sh 'ls -la'
      }
    }
  }
}

