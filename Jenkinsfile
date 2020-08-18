pipeline {
  agent any
  triggers {
    // Trigger once a day on the 1st and 15th of every month
    cron('H H 1,15 * *')
  }
  stages {
    stage('Checkout repository') {
      steps {
        checkout scm
      }
    }
    stage('Build amd64 SDK for host amd64') {
      steps {
        sh 'sudo ./usdk-target-build -a amd64 -b amd64 -f ubuntu-sdk-16.04'
      }
    }
    stage('Build armhf SDK for host amd64') {
      steps {
        sh 'sudo ./usdk-target-build -a armhf -b amd64 -f ubuntu-sdk-16.04'
      }
    }
    stage('Build arm64 SDK for host amd64') {
      steps {
        sh 'sudo ./usdk-target-build -a arm64 -b amd64 -f ubuntu-sdk-16.04'
      }
    }
    stage('Build arm64 SDK for host arm64') {
      steps {
        sh 'sudo ./usdk-target-build -a arm64 -b arm64 -f ubuntu-sdk-16.04'
      }
    }
    stage('Build armhf SDK for host armhf') {
      steps {
        sh 'sudo ./usdk-target-build -a armhf -b armhf -f ubuntu-sdk-16.04'
      }
    }
    stage('Publish SDK') {
      when { branch 'master' }
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
