pipeline {
    agent any

    stages {
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
        stage ('Deploy'){
           steps{
              deploy adapters: [tomcat9(credentialsId: 'e13c384a-9384-4d80-9230-ee41d35381cf', path: '', url: 'http://localhost:9090/')], contextPath: null, war: '**/*.war'
           }
        }
    }
}