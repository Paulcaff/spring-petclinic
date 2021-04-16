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
       stage("Push Docker"){
              steps{
                sshagent(['awsKey']) {
                           // some block
                           sh "ssh -o StrictHostKeyChecking=no ec2-user@34.245.78.133 docker stop pet_clinic || true"
                           sh "ssh -o StrictHostKeyChecking=no ec2-user@34.245.78.133 docker rm pet_clinic || true"
                           sh "ssh -o StrictHostKeyChecking=no ec2-user@34.245.78.133 docker rmi \$(docker images -a -q) || true"
                           sh "ssh -o StrictHostKeyChecking=no ec2-user@34.245.78.133 docker run -p 8080:8080 -d --name pet_clinic paulcaff/petclinic:0.1"
                       }

                  }

              }
   }
}

