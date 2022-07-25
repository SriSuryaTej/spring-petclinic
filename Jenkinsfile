pipeline{
    triggers{
        cron ""*/8 * * * *""
    }  
    agent{ label 'K8s'}
    stages{
        stage('Deploying application') {
            steps{
                   sh 'kubectl apply -f spc-prod.yaml'

                }
        }
    }
}