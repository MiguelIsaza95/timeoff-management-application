pipeline {
  agent any

  tools { nodejs }
    
  stages {
    stage('Install') {
      steps {
        sh "npm install"
      }
    }      
    stage('Test') {
      steps {
        sh "node test"
      }
    }
    stage('buildArtifact'){
      steps {
        sh "echo build"
      }
    }
  }
}