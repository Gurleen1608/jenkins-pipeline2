pipeline {
    agent any

    stages {
    
        stage("CI/CD: Warm Up"){
            steps {
                script {
                    sh "java -version"

                }
            }
        }
		
		stage("Checkout from SCM"){
            steps {
                script {
                    sh "git clone https://github.com/gurleen1608/jenkins-pipeline2.git"				
                }
            }
        }

        stage('Build ') {
            steps {
            script {
                sh "cd ${WORKSPACE}/jenkins-pipeline2 "
                sh "cd jenkins-pipeline2 && mvn clean install "
            }
        }
        }
	     stage ('Code Quality') {
        steps {
            withSonarQubeEnv('SonarQube') {
            sh 'mvn -f pom.xml sonar:sonar'
            }
      }
    }
	     stage ('Nexus upload') {
                steps {
                           nexusArtifactUploader artifacts: [[artifactId: 'gs-spring-boot-docker', classifier: '', file: 'target/gs-spring-boot-docker-0.1.0.jar', type: 'jar']], credentialsId: '9cf4cc05-391a-4b8b-a5c4-5c17285c1d52', groupId: 'org.springframework.boot', nexusUrl: '65.2.39.239:8081/', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snapshots', version: '0.1.0-SNAPSHOT'
 
                }
        
            }
	    
	   
	   

        stage('Verify ') {
            steps {
            script {
                sh "cd ${WORKSPACE}/jenkins-pipeline2 "
                sh "ls -lhrt jenkins-pipeline2 "
            }
        }
        }        
        
		}
		
     post { 
         always { 
            cleanWs()
         }
    }		
}
