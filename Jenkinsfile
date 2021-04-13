pipeline {
   agent any
   stages{
   stage('Build') {
   steps{bat 'mvn clean package'}
   }
   stage('Results') {
      steps{
      junit '**/target/surefire-reports/TEST-*.xml'
      archiveArtifacts 'target/*.jar'
      }
   }
   }
}
