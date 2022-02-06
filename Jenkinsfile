pipeline{
  agent any
    stages{
      stage('scm checkout'){
        steps{
          git clone url
        }
        stage('maven build'){
          steps{
            sh 'mvn -B -DskipTests clean install'
          }
        }
      }
    }
