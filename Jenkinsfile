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
        stage ('QA Deploy')  {
         echo "deploying to QA Env " 
           deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://13.235.50.71:8080')], contextPath: null, war: '**/*.war'

        }
        stage ('QA Approve')  {
           echo "Taking approval from QA manager"

             timeout(time: 7, unit: 'DAYS') {
             input message: 'Do you want to proceed to PROD?', submitter: 'mail4avitesh@gmail.com'
              }
        }
        stage ('Staging Deployment'){
            steps {
                build job: 'vprofile-deply-to-stage'
            }
            
        }
        }


}
