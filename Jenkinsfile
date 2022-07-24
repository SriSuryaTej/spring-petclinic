pipeline{  
    agent any
    stages{
        stage('Docker Build') {
        agent{ label 'docker' }    
                steps {
                   sh 'docker build -t spring-petclinic:latest .'
      }
    }
        stage('Docker Push') {
            agent{ label 'docker' }
                steps {
                   withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
                   sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                   sh 'docker tag spring-petclinic:latest optimussurya/project_repo:spring-petclinic'
                   sh 'docker push optimussurya/project_repo:spring-petclinic'
        }
      }
    }
        stage('Pulling Docker Image'){
            agent{ label 'k8s'}
            when{
                branch 'dev'
            }
                steps{
                   sh 'kubectl apply -f spc_dev.yaml'

                }
            }
        stage('Pulling Docker Image'){
            agent{ label 'k8s'}
            when{
                branch 'qa'
            }
                steps{
                   sh 'kubectl apply -f spc_qa.yaml'

                }
            }
        stage('Pulling Docker Image'){
            agent{ label 'k8s'}
            when{
                branch 'staging'
            }
                steps{
                   sh 'kubectl apply -f spc_staging.yaml'

                }
            }
        stage('Pulling Docker Image'){
            agent{ label 'k8s'}
            when{
                branch 'prod'
            }
                steps{
                   sh 'kubectl apply -f spc_prod.yaml'

                }
            }
  }
}