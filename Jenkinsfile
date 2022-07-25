pipeline{  
    agent{ label 'K8s'}
    stages{
        stage('Deploying application') {
            steps{
                   sh 'kubectl apply -f spc-prod.yaml'

                }
        }
    }
}