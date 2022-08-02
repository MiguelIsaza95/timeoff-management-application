pipeline {
  agent any

  environment {
      version = "${env.BUILD_ID}"
      dockerimagename = "us-east1-docker.pkg.dev/devops-challenge-357700/dockerchallenge/timeoffapp"
      dockerimage = ""
      project = "devops-challenge-357700"
      region = "us-central1"
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
            script {
                dockerImage = docker.build dockerimagename
            }
        }
    }
    stage('Publish artifac'){
        steps{
            script{
                withCredentials([file(credentialsId: 'gcp_creds', variable: 'dockerlogin')]){
                    sh '''
                    chmod 600 $dockerlogin
                    cat $dockerlogin | docker login -u _json_key --password-stdin https://us-east1-docker.pkg.dev
                    '''
                    dockerImage.push("latest")
                    dockerImage.push("${env.BUILD_ID}")
                }
            }
        }
    }
    stage('Deploy app to GKE'){
        steps{
            script{
                withCredentials([file(credentialsId: 'gcp_creds', variable: 'gauth')]){
                    sh '''
                    gcloud auth activate-service-account --key-file=$gauth
                    gcloud container clusters get-credentials ${project}-gke --region ${region} --project ${project}
                    kubectl apply -f ./deployment.yaml
                    kubectl apply -f service.yaml
                    '''
                }
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