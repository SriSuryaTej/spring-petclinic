pipeline{  
    agent{ label 'k8s'}
    stages{
        stage("SCM") {
            git 'https://github.com/SriSuryaTej/spring-petclinic.git'
        }
        stage('Deploying application') {
            steps{
                   sh 'kubectl apply -f spc_dev.yaml'

                }
        }
    }
}