pipeline {
    agent { label 'JDK11_MVN' }
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
                    serverId: 'JFROG_OSS',
                    releaseRepo: 'surya-maven-releases',
                    snapshotRepo: 'surya-maven-snapshots'
                )
                
            }
        }
        stage ('Exec Maven') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'JFROG_OSS', usernameVariable: 'admin', passwordVariable: 'Jfrog@123')]) {
                    rtMavenRun (
                        tool: 'MVN_3.8.5', 
                        pom: 'pom.xml',
                        goals: 'clean package',
                        deployerId: "MAVEN_DEPLOYER"
                    )
                    stash includes: '**/*.jar', name: 'spcjar'
                }
            }
        }
        stage('Quality Check'){
             steps {
                withSonarQubeEnv(installationName: 'SONAR_SCANNER', envOnly: true, credentialsId: 'SONAR_TOKEN') {
                    sh "mvn clean package sonar:sonar"
					echo "${env.SONAR_HOST_URL}"
                    }
                }
            }
        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: 'JFROG_OSS'
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

