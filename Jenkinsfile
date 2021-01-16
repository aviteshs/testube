pipeline {
  	agent any
    stages{
        stage('Build'){
            steps {
                sh 'mvn install'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }		
                stage ('code artificat to nexus job'){
            steps {
                sh 'cp /var/lib/jenkins/workspace/vprpofile-pipeline/target/vprofile-v2.war /var/lib/jenkins/workspace/vprofile-nexus-versoning/vprofile-v2.war'
            }  
           post {
               success {
                    echo 'artificats copy'
               }
           }
        }
        stage ('Nexus Versioning'){
            steps {
                build job: 'vprofile-nexus-versoning'
            }  
        }

          stage ('code artificat to deploy staging'){
            steps {
                sh 'cp /var/lib/jenkins/workspace/vprpofile-pipeline/target/vprofile-v2.war /var/lib/jenkins/workspace/vprofile-deply-to-stage/vprofile-v2.war'
            }  
           post {
               success {
                    echo 'artificats copy'
               }
           }
        }
        
        stage ('Staging Deployment'){
            steps {
                build job: 'vprofile-deply-to-stage'
            }
            
        }
        }


}
