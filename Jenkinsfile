pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'ls -lart'
      }
    }
    stage('testing and build') {
      parallel {
        stage('firefox') {
          steps {
            echo 'firefox testing'
          }
        }
        stage('internet explorer') {
          steps {
            echo 'IE testing'
          }
        }
        stage('chrome') {
          steps {
            echo 'chrome testing'
          }
        }
      }
    }
    stage('Approval') {
      steps {
        input id: 'Required approval', message: 'Enter a password to proceed', ok: 'Approve', submitter: 'mjimenez'
      }
    }
    stage('Finished') {
      steps {
        s3Download bucket: 'aws-nested-templates', file: 'sg-rules.json'
        sh 'ls -lart'
        sh 'cat sg-rules.json'
        echo 'The end!'
      }
    }
  }
}
