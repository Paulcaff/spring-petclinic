pipeline {
   agent any
   stages{
   stage('Build') {
   steps{bat('mvn clean package')}
      // Run the maven build
//       withEnv(["MVN_HOME=$mvnHome"]) {
//          if (isUnix()) {
//             sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package'
//          } else {
//             bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
//          }
//       }
   }
   stage('Results') {
      steps{
      junit '**/target/surefire-reports/TEST-*.xml'
      archiveArtifacts 'target/*.jar'
      }
   }
   }
}