pipeline {
   options {
    buildDiscarder(logRotator(numToKeepStr: '50', artifactNumToKeepStr: '50'))
  }
agent any 
stages {
   stage ('compile stage') {
   steps {
    sh 'mvn compile'
    }
   }
   stage ('test stage') {
   steps {
   sh 'mvn test'
     }
   }
   stage('Sonarqube analysis') {
    steps {
    script {
             scannerHome = tool 'SonarScanner';
        }
     withSonarQubeEnv('SonarQube') {
         bat "${scannerHome}/bin/sonar-scanner.bat" 
      }
    }
  }
   stage ('package') {
   steps {
      sh 'mvn package'
      }
   }
   stage ('Deploying to Nexus') {
   steps {
      sh 'mvn deploy'
      }
   }
 }
   post {
        always {
            archiveArtifacts artifacts: '**/*.jar', fingerprint: true
            archiveArtifacts artifacts: 'target/***', fingerprint: true
           junit 'target/surefire-reports/*.xml'
        }
    }
}
