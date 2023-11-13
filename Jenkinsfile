pipeline{
    agent any

    stages{
        stage ('Build'){
            steps{
                sh 'mvn clean package'
            }
            post{
                SUCCESS{
                    echo 'Archiving the artifacts'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deloy to Tomcat server'){
            steps{
                deploy adapters: [tomcat9(credentialsId: 'Tomcat_cred', path: '', url: 'http://192.168.56.101:8090/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
