pipeline {
    agent any
    tools {
        maven 'Maven' 
        }
    stages {
        stage('Build Application') {
            steps {
                bat 'mvn -f pom.xml clean package'
            }
        
            post {
                success {
                    echo "Now Archiving the Artifacts....."
                    archiveArtifacts artifacts: '**/*.war'
                }
              }
            }
            stage(Deployment On Test) {
                steps {
                    deploy adapters: [tomcat8(credentialsId: 'credtomcat', path: '', url: 'http://54.159.195.182:8090')], contextPath: 'spring-boot-war-example', war: '**/*.war'

                }
            }
         }   
            post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}
