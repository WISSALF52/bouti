
pipline{
    node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def mvn = tool 'maven';
    withSonarQubeEnv() {
    bat "\"${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=tique -Dsonar.projectName='tique'
    }
  }
}}
