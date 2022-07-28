pipeline {
  agent any

  tools { 
      nodejs '13.0.0' 
      }
    
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