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
   stage("Push Docker"){
       steps{
           withCredentials([string(credentialsId: 'dockerpassword', variable: 'dockerpassword')]) {
               bat "docker login -u paulcaff -p ${dockerpassword}"
           }
           bat 'docker push paulcaff/petclinic:0.1'
       }
   }
}
}
