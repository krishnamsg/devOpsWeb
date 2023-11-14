pipeline {
    agent any
    
    //tools {
        //maven 'local_maven'
    parameters {
         string(name: 'staging_server', defaultValue: '192.168.56.101', description: 'Remote Staging Server')
    }

stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Archiving the artifacts'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deployments'){
            parallel{
                stage ("Deploy to Staging"){
                    steps {
                        sudo cp -r **/*.war /opt/tomcat/webapps/
                    }
                }
            }
        }
    }
}
