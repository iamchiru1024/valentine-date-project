pipeline{
    agent any

    stages {
        
        stage('Checkout from Git'){
            steps{
                git branch: 'main', url: 'https://github.com/iamchiru1024/valentine-project.git'
            }
        }
        stage('TRIVY FS SCAN') {
            steps {
                sh "trivy fs . > trivyfs.txt"
            }
        }
        stage("Docker Build & Tag Docker Image"){
            steps{
                script{
                   withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker'){   
                       sh "docker build -t chirru1024/valentinesdays:v1 ."
                    }
                }
            }
        }
        stage("TRIVY Image Scan"){
            steps{
                sh "trivy image chirru1024/valentinesdays:v1 > trivy.txt" 
            }
        }
        stage('Docker push'){
            steps {
                script{
                   withDockerRegistry(credentialsId: 'docker-creds', toolName: 'docker'){   
                       sh "docker push chirru1024/valentinesdays:v1"
              }
          }
      }
   }
        stage('Deploy container'){
            steps {
                 sh "docker run -d -p 8081:80 chirru1024/valentinesdays:v1"
            }
        }
    }
}
