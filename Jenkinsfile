pipeline{  
    agent{ label 'K8s'}
    stages{
        stage('Deploying application'){
            when {
                branch 'main'
            }
            steps{
                   sh 'kubectl apply -f spc-dev.yaml'
                }
        }
    }
}