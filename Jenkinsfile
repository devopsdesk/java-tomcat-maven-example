pipeline{
  agent any
      tools {
    maven 'maven3.8.4'
      }
    stages{
      stage('scm checkout'){
        steps{
          git credentialsId: 'b8b62064-a75f-4d4a-b3ce-acd517159d66', url: 'https://github.com/devopsdesk/java-tomcat-maven-example.git'
        }
      }
        stage('maven build'){
          steps{
            sh 'mvn -B -DskipTests clean install'
          }
        }
         stage('Push Docker Image'){
        withCredentials([string(credentialsId: 'Docker_Hub_Pwd', variable: 'Docker_Hub_Pwd')]) {
          sh "docker login -u devopsdesk -p ${Docker_Hub_Pwd}"
        }
        sh 'docker push devopsdesk/java-web-app:v1'
     }     
    }
   }
