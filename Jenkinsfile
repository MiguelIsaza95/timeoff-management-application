pipeline {
  agent any

  tools { 
      nodejs 'node' 
      }
    
  stages {
    stage('Install') {
      steps {
        sh "npm install"
        sh "npm install sqlite3 --save"
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