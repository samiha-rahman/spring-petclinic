pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'mvn compile'
      }
    }

    stage('Test') {
      steps {
        sh 'mvn test'
      }
    }

    stage('Package') {
      steps {
        sh 'mvn package'
      }
    }
    
    stage('Deploy') {
      when {
        branch 'master'
      }
      steps {
        sh 'mvn package'
      }
    }
  }
  post {
    failure {
        mail to: 'hellosamiha@gmail.com',
             subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
             body: "Something is wrong with ${env.BUILD_URL}"
    }
    success {
        mail to: 'hellosamiha@gmail.com',
             subject: "Passing Pipeline: ${currentBuild.fullDisplayName}",
             body: "Everything is good with ${env.BUILD_URL}"
    }
}
}
