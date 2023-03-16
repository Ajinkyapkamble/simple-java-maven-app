pipeline {
    agent any
    
    stages {
        stage('SCM Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Ajinkyapkamble/simple-java-maven-app.git'
            }
        }
        
        stage('Maven Build') {
            steps {
                sh 'mvn clean install -DbuildNum=$BUILD_NUMBER'
            }
            post {
                success {
                    archiveArtifacts artifacts: 'target/*.jar', allowEmptyArchive: true
                }
            }
        }
        
        stage('Deploy') {
            steps {
                sh 'cp target/*.jar /var/lib/tomcat9/webapps/'
            }
        }
    }
}
