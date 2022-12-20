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
               deploy adapters: [tomcat8(credentialsId: '8e222ae8-093f-4022-b144-08fb01d3b22a', path: '', url: 'http://127.0.0.1:8080/')], contextPath: null, war: '**/*.war'
           }
        }
    }
}