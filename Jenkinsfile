pipeline {
   agent any
   stages{
    stage('Build') {
        steps{
            bat 'mvn -version'
            bat 'mvn clean package'
            }
        }
   stage('Results') {
      steps{
        junit '**/target/surefire-reports/TEST-*.xml'
        archiveArtifacts 'target/*.jar'
        }
      }
   stage('Docker') {
         steps{
           bat 'docker build -t paulcaff/petclinic:0.1 .'
         }
   }
}
}
