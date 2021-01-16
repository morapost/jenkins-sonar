pipeline {
    agent any
    environment {
        mvnHome = tool name: 'maven-3', type: 'maven'
    }
    
    stages {

        stage('Git checkout') {
            steps {
                git credentialsId: 'github-login', url: 'https://github.com/morapost/jenkins-sonar', branch: 'main'
            }
        }

        stage ('Build') {
            steps {
                
                sh "${mvnHome}/bin/mvn clean package"
            }
            
        }   
        stage ('SonarQube Analysis') {
            steps {
                    withSonarQubeEnv('sonar') {
                      sh "${mvnHome}/bin/mvn package sonar:sonar"
                  }
        }
        
    }
}


