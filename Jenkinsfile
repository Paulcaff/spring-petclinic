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
       stage("aws"){
              steps{ echo "here steps"
                sshagent(['awskey']) {
                           // some block
                           //sh "ssh -o StrictHostKeyChecking=no ec2-user@34.240.121.213 docker stop pet_clinic || true"
                           //sh "ssh -o StrictHostKeyChecking=no ec2-user@34.240.121.213 docker rm pet_clinic || true"
                           //sh "ssh -o StrictHostKeyChecking=no ec2-user@34.240.121.213 docker rmi \$(docker images -a -q) || true"

                           //sh "ssh -o StrictHostKeyChecking=no ec2-user@34.240.121.213 docker run -p 8080:8080 -d --name pet_clinic paulcaff/petclinic:0.1"
                           echo "here2"

                       }

                  }

              }
       stage('Email Build Status'){
           steps{
               emailext to: 'paul.cafferkey@students.ittralee.ie', body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} More info at: ${env.BUILD_URL}", subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
           }
       }
   }
}

