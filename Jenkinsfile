pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'mvn build'
      }
    }

    stage('Test') {
      steps {
        sh './mvnw test'
      }
    }

    stage('Package') {
      steps {
        sh './mvnw package'
      }
    }

  }
}