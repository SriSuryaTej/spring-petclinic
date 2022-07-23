pipeline{  
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
 
  }
}