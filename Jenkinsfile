pipeline {
   agent any

   stage('Build') {
   steps{bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)}
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

      junit '**/target/surefire-reports/TEST-*.xml'
      archiveArtifacts 'target/*.jar'
   }
}
