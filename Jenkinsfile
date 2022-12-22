pipeline{
    agent any
    environment {
    def MavenHome = tool name:'MAVEN-3.8.6', type:'maven'
    }
    stages{
       stage('GitClone'){
            steps{
                 git 'https://github.com/NVTechnologies/java-app.git'
            }
         }        
       stage('Build'){
            steps{
                sh "${MavenHome}/bin/mvn clean package"
            }
         }
        stage('SonarQube analysis') {
//    def scannerHome = tool 'SonarScanner 4.0';
        steps{
        withSonarQubeEnv('sonarqube-8.9.10') { 
        sh "${MavenHome}/bin/mvn sonar:sonar"
    }
        }
        }
       
    }
}
