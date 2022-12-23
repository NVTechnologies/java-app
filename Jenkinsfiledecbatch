pipeline{
    agent any
    environment {
    def MavenHome = tool name:'MAVEN-3.8.6', type:'maven'
    }
    stages{
       stage('GitClone'){
            steps{
                 git 'https://github.com/NVTechnologies/java-maven-application.git'
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
        stage('Upload war package to Nexus'){
            steps{
                script{
                   nexusArtifactUploader artifacts: 
                   [
                       [
                           artifactId: 'maven-project', 
                           classifier: '', 
                           file: 'webapp/target/webapp.war', 
                           type: 'war'
                           
                           ]
                        ], 
                           
                           credentialsId: 'nexus-credentials', 
                           groupId: 'com.example.maven-project', 
                           nexusUrl: '15.207.120.123:8081/', 
                           nexusVersion: 'nexus3', 
                           protocol: 'http', 
                           repository: 'java-maven-release', 
                           version: '1.0.0'
                }
            }
       }
       
    }
}
