pipeline{  
    agent{ label 'K8s'}
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
                   sh 'docker tag spring-petclinic:latest optimussurya/spring-petclinic:$BUILD_NUMBER'
                   sh 'docker push optimussurya/spring-petclinic:$BUILD_NUMBER'
                   sh 'docker tag spring-petclinic:latest optimussurya/spring-petclinic:latest'
                   sh 'docker push optimussurya/spring-petclinic:latest'
            }
          }
        }
        stage('') {
            
        }
        stage('Deploying application'){
            steps{
                   sh 'kubectl apply -f spc-dev.yaml'
                }
        }
    }
}
        