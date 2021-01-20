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
          deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://10.128.15.219:9090/')], contextPath: null, war: 'target/calculator.war'
      }
    }
  }
}
