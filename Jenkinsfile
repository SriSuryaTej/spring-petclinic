pipeline {
    agent { label 'JDK11_MVN_SONAR_JFROG' }
	tools {
		maven 'MVN_3.8.5'
	}
    stages {
        stage('scm') {
            steps {
                git url: 'https://github.com/SriSuryaTej/spring-petclinic.git', branch: 'declarative'
            }
        }
        stage ('Artifactory configuration') {
            steps {
                rtMavenDeployer (
                    id: "MAVEN_DEPLOYER",
                    serverId: 'JFROG-OSS',
                    releaseRepo: 'surya-maven-releases',
                    snapshotRepo: 'surya-maven-snapshots'
                )
                
            }
        }
        stage ('Exec Maven') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'JFROG_ARTIFACTORY', usernameVariable: 'ARTIFACTORY_USERNAME', passwordVariable: 'ARTIFACTORY_PASSWORD')]) {
                    rtMavenRun (
                        tool: 'MVN_3.8.5', 
                        pom: 'pom.xml',
                        goals: 'clean install',
                        deployerId: "MAVEN_DEPLOYER"
                    )
                    stash includes: '**/*.jar', name: 'spcjar'
                }
            }
        }
        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: 'JFROG-OSS'
                )
            }
        }
        stage ('copy to other node') {
            agent { label 'MASTER'}
            steps {
                unstash 'spcjar'
            }
        }
    }
}