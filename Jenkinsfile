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
      }
    }
