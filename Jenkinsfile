pipeline {
  agent any

  tools { 
      nodejs 'node' 
      }
    
  stages {
    stage('Install') {
      steps {
        sh "npm install"
      }
    }      
    stage('Test') {
      steps {
        sh "npm test"
      }
    }
    stage('buildArtifact'){
      steps {
        sh "echo build"
      }
    }
  }
}