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
           junit 'target/surefire-reports/*.xml'
        }
        success {
            archiveArtifacts artifacts: '**/*.jar', fingerprint: true
            archiveArtifacts artifacts: 'target/***', fingerprint: true
        }
        failure {
            mail to: naredla.ramireddy@gmil.com, subject: 'The Pipeline failed :('
        }
        unstable {
            echo 'JENKINS PIPELINE WAS MARKED AS UNSTABLE'
        }
        changed {
            echo 'JENKINS PIPELINE STATUS HAS CHANGED SINCE LAST EXECUTION'
        }
    }
}
