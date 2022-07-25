pipeline{
    triggers{
        cron ""*/2 * * * *""
    }
    agent{ label 'K8s'}
    stages{
        stage('Deploying application') {
            steps{
                   sh 'kubectl apply -f spc-qa.yaml'

                }
        }
    }
}