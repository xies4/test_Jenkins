pipeline {
  agent { label 'Jenkins-Build-Node-01' }
  
  stages {
    stage('TEST') {
      steps {
        checkout scm
        echo 'Jenkinsfile is running'
        sh 'pwd'
        sh 'git rev-parse --short HEAD'
        sh 'ls -la'
      }
    }
  }
}

