pipeline {

  agent any
  environment {
    imagename = "pbeniwal/democalc:v$BUILD_NUMBER"
    registryCredential = 'docker'
    dockerImage = ''
  }

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

    stage ('Building image')  {
      steps {
        script {
          dockerImage = docker.build imagename
        }
      }
    }

    stage ('Push Image') {
      steps {
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }

   stage ('Running Container')  {
      steps {
        script {
          sh 'docker rm --force tomcat9999 && echo 1'
          dockerImage.run('--name tomcat9999 -p 9999:8080')
        }
      }
    }

  }
}
