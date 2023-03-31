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
                    sh "git clone https://github.com/Dewank7852/jenkins-pipeline2.git"				
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
                           nexusArtifactUploader artifacts: [[artifactId: 'gs-spring-boot-docker', classifier: '', file: 'target/${project.build.finalName}.jar', type: 'jar']], credentialsId: '6ff32036-ec16-4226-9c57-b84ad15d96a5', groupId: 'org.springframework.boot', nexusUrl: '35.93.98.52:8081/', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snapshots', version: '2.0.2.RELEASE'
 
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
