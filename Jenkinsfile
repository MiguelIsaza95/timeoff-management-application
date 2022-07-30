pipeline {
  agent any

  environment {
      version = "${env.BUILD_ID}"
      dockerimagename = "us-east1-docker.pkg.dev/devops-challenge-357700/dockerchallenge/challengeapp:latest"
      dockerimage = ""
      }

  tools { 
      nodejs 'node' 
      }
    
  stages {
    stage('Install') {
      steps {
        sh '''
        npm i
        '''
      }
    }      
    stage('Test') {
      steps {
        sh '''
        npm test
        '''
      }
    }
    stage('build'){
      steps {
        sh "npm run build -y"
      }
    }
    stage('Create Docker Artifac'){
        steps {
            sh '''
            npx google-artifactregistry-auth
            '''
            script {
                dockerImage = docker.build dockerimagename
            }
        }
    }
    stage('Publish artifac'){
        steps{
            script{
                ocker.withRegistry('https://us-east1-docker.pkg.dev', 'devops-challenge-357700'){
                    dockerImage.push()
                }
            }
        }
    }
    stage('Deploy app to GKE'){
        steps{
            script{
                kubernetesDeploy (kubeconfigId: 'kubernetes', configs: 'deployment.yaml')
                kubernetesDeploy (kubeconfigId: 'kubernetes', configs: 'service.yaml')
            }
        }
    }
  }
  
  post { 
      always { 
          cleanWs()
        }
    }
}