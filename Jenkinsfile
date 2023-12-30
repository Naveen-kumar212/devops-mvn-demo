pipeline{
    agent any
/*    
    tools {
         maven 'maven'
         jdk 'java'
    }
*/
    environment {
        PATH = "/usr/share/maven/bin#:$PATH"
    }
    stages{
        stage('Git Checkout'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'Jenkins-demo', url: 'https://github.com/Naveen-kumar212/devops-mvn-demo.git']]])
            }
        }
        stage('mvn clean'){
            steps{
              sh  'mvn clean'
            }
        }
        stage('mvn compile'){
            steps{
               sh 'compile'
            }
        }
        stage('mvn package'){
            steps{
               sh 'mvn package'
            }
        }
    }
     post {
        success {
            emailext (
                subject: "Job success '${env.JOB_NAME}' - Build # ${env.BUILD_NUMBER} - Successful",
                body: "SUCCESS: Job '${env.JOB_NAME}' - Build # ${env.BUILD_NUMBER} is successful. Check console output at ${env.BUILD_URL}",
                to: "ligidnex@gmail.com",
            )
        }
        failure {
            emailext (
                subject: "Job '${env.JOB_NAME}' - Build # ${env.BUILD_NUMBER} - Failed",
                body: "FAILURE: Job '${env.JOB_NAME}' - Build # ${env.BUILD_NUMBER} failed. Check console output at ${env.BUILD_URL}",
                to: "ligidnex@gmail.com",
            )
        }
    }
}
