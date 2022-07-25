pipeline{  
    agent{ label 'K8s'}
    stages{
        stage('Deploying application'){
            steps{
                   sh "kubectl create namespace dev"
                   sh 'kubectl apply -f spc-dev.yaml'

                }
        }
    }
}