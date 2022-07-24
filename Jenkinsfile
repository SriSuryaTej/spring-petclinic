pipeline{ 
    agent{ label 'docker' } 
    stages{
        stage('Docker Build') {
            
                steps {
                   sh 'docker build -t spring-petclinic:latest .'
      }
    }
        stage('Docker Push') {
          
                steps {
                   withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
                   sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                   sh 'docker tag spring-petclinic:latest optimussurya/project_repo:spring-petclinic'
                   sh 'docker push optimussurya/project_repo:spring-petclinic'
        }
      }
    }
    }
    
    agent { label 'K8s' }
    stages {
        stage('Pulling Docker Image') {
            when{
                branch 'dev'
            }
                steps{
                   sh 'kubectl apply -f spc_dev.yaml'

                }
            }
        stage('Pulling Docker Image') {
          
            when{
                branch 'qa'
            }
                steps{
                   sh 'kubectl apply -f spc_qa.yaml'

                }
            }
        stage('Pulling Docker Image') {
            when{
                branch 'staging'
            }
                steps{
                   sh 'kubectl apply -f spc_staging.yaml'

                }
            }
        stage('Pulling Docker Image') {
            when{
                branch 'prod'
            }
                steps{
                   sh 'kubectl apply -f spc_prod.yaml'

                }
            }
  }
}
