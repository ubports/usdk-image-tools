pipeline {
  agent any
  triggers {
    // Trigger once a day on the 1st and 15th of every month
    cron('H H 1,15 * *')
  }
  stages {
    stage('Build SDK') {
      steps {
        checkout scm
        sh 'sudo ./usdk-target-build -a armhf -b amd64 -f ubuntu-sdk-16.04'
      }
    }
    stage('Publish SDK') {
      steps {
        sh './publish_image_bundle'
      }
    }
  }

  post {
      always {
          cleanWs()
      }
  }
}
