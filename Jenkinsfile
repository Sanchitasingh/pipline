pipeline{
    agent any
    tools{
        maven 'Maven'
    }

    stages{
        stage ('Build'){
            steps{
                sh 'mvn clean package'
            }
            post{
                success{
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: '**/target/*.war' 
                }
            }
        }
        stage ('Deploy to tomcat server') {
           steps{
               deploy adapters: [tomcat8(credentialsId: '45f75e53-18fb-4659-b2c3-547e4763d7ba', path: '/manager', url: 'http://localhost:8080/')], contextPath: null, onFailure: false, war: '**/*.war'
           }
        }
    }
}
