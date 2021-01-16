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
        stage ('Nexus Versioning'){
            steps {
                build job: 'vprofile-nexus-versoning'
            }  
        }

        stage ('Staging Deployment'){
            steps {
                build job: 'vprofile-deply-to-stage'
            }
            
        }
        }


}
