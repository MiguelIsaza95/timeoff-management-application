pipeline {
  agent any
    
  stages {
     
    stage('Install') {
      steps {
        sh 'npm install'
      }
    }  
            
    stage('Test') {
      steps {
        sh 'node test'
      }
    }
    stage('buildArtifact')
    steps {
        sh ''
    }
  }
}