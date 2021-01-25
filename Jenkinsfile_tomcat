pipeline {

  agent any
  stages {
    stage('Compile') {
      steps{
        sh 'mvn clean compile'
      }
    }
    
    stage('Unit Test') {
      steps{
        sh 'mvn clean test'
      }
    }

    stage('Package') {
      steps{
        sh 'mvn clean install'
      }
    }

    stage('ContDelivery') {
      steps{
          deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://localhost:9090/')], contextPath: null, war: 'target/calculator.war'
      }
    }
  }
}
