pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh './mvnw build'
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