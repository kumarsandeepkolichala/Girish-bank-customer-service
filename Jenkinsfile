pipeline {
  agent any
  tools { 
       // maven 'Maven'
        jdk 'JAVA_HOME'
  }
  stages {
    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace... */
      steps {
        checkout scm
      }
    }
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
        sh 'echo $USER'
        sh 'echo whoami'
      }
    }
    stage('Docker Build') {
      steps {
        sh '/usr/bin/docker build -t kumarsandeeokolichala@gmail.com/bank-customer-service:latest .'
      }
    }
    stage('Push image') {
      steps {
        withDockerRegistry([credentialsId: 'docker-hub', url: "http://261167483116.dkr.ecr.us-east-2.amazonaws.com/girish"]) {
          sh '/usr/bin/docker push girish99/bank-customer-service:latest'
        }
      }
    }
  }
}
