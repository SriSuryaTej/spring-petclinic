pipeline{
    triggers{
        cron ""*/3 * * * * ""
    }  
    agent{ label 'K8s'}
    stages{
        stage('Deploying application') {
            steps{
                   sh 'kubectl apply -f spc-staging.yaml'

                }
        }
    }
}