pipeline{  
    agent{ label 'k8s'}
    stages{
        stage("SCM") {
            git 'https://github.com/SriSuryaTej/spring-petclinic.git'
        }
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
        stage('Pulling Docker Image'){
        when{
                branch 'dev'
            }
                steps{
                   sh 'kubectl apply -f spc_dev.yaml'

                }
            }
        stage('Pulling Docker Image'){
            when{
                branch 'qa'
            }
                steps{
                   sh 'kubectl apply -f spc_qa.yaml'

                }
            }
        stage('Pulling Docker Image'){
            when{
                branch 'staging'
            }
                steps{
                   sh 'kubectl apply -f spc_staging.yaml'

                }
            }
        stage('Pulling Docker Image'){
            when{
                branch 'prod'
            }
                steps{
                   sh 'kubectl apply -f spc_prod.yaml'

                }
            }
  }
}