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
          stage('Build Docker Image'){
            steps{
        sh 'docker build -t devopsdesk/java-web-app:v1 .'
    }
          }
         stage('Push Docker Image'){
           steps{
        withCredentials([string(credentialsId: 'Docker_Hub_Pwd', variable: 'Docker_Hub_Pwd')]) {
          sh "docker login -u devopsdesk -p ${Docker_Hub_Pwd}"
        }
        sh 'docker push devopsdesk/java-web-app:v1'
     }  
         }
           stage('Run Docker Image In Dev Server'){
             steps{
        
        def dockerRun = ' docker run  -d -p 8080:8080 --name java-web-app devopsdesk/java-web-app'
             
         sshagent(['DOCKER_SERVER']) {
          sh 'ssh -o StrictHostKeyChecking=no ec2-user@13.233.252.164 docker stop java-web-app || true'
          sh 'ssh  ec2-user@13.233.252.164 docker rm java-web-app || true'
          sh 'ssh  ec2-user@13.233.252.164 docker rmi -f  $(docker images -q) || true'
          sh "ssh  ec2-user@13.233.252.164 ${dockerRun}"
       } 
             }
           }
    }
   }
