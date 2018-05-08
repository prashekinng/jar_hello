pipeline {
   options {
    buildDiscarder(logRotator(numToKeepStr: '2', artifactNumToKeepStr: '2'))
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
            archiveArtifacts artifacts: '**/*.jar', fingerprint: true
        }
    }
}
