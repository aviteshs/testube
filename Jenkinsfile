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
                Build job: 'vprofile-nexus-versoning'
            }
            
        }

        stage ('Staging Deployment'){
            steps {
                Build job: 'vprofile-deply-to-stage'
            }
            
        }
        
    }


}
