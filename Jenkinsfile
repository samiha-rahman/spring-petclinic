pipeline {
  agent any
  stages {
    stage('Check master') {
      when {
        not {branch 'master'}
      }
      steps {
        exit 0
      }
    }
    
    stage('Check eigth commit') {
      steps {
        script {
          int commits = sh(returnStdout: true, script: "git rev-list master --count origin/master")
          if (!(commits % 8 == 0)){
            error("Not the 8th commit!")
            exit 0
          }
        }
      }
    }
      
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
        slackSend (color: 'danger', message: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
    }
    success {
        slackSend (color: 'good', message: "PASSED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
    }
}
}
