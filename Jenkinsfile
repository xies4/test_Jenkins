pipeline {
  agent any

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