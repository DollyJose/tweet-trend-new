pipeline {
    agent {
        node{
           label 'maven'
        }
    }
environment {
    PATH = "/opt/apache-maven-3.9.6/bin:$PATH"
}
    stages {
        stage("build"){
          steps{
            echo "--------build started--------"
            sh 'mvn clean deploy -Dmaven.test.skip=true'
            echo "--------build completed--------"
          }
        }
        stage("test"){
          steps{
            echo "--------unit test started-----"
            sh 'mvn surefire-report:report'
            echo "--------unit test completed------"
          }
        }
        stage('SonarQube analysis') {
         environment{
         scannerHome = tool 'sonar-scan';
         }
         steps{
           withSonarQubeEnv('sonarqube-server') { // If you have configured more than one global server connection, you can specify its name
           sh "${scannerHome}/bin/sonar-scanner"
        }
       }
      }  
    }
   }
