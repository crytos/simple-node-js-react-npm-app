pipeline {
  agent {
    docker {
      image 'node:8-alpine'
      args '''--name react\\
    --env "VIRTUAL_HOST=react.mastertest.cf" \\
    --env "VIRTUAL_PORT=3000" \\
    --env "LETSENCRYPT_HOST=react.mastertest.cf" \\
    --env "LETSENCRYPT_EMAIL=juliusmubajje1@gmail.com" \\'''
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }
    stage('Test') {
      environment {
        CI = 'true'
      }
      steps {
        sh './jenkins/scripts/test.sh'
      }
    }
    stage('Deliver') {
      steps {
        sh './jenkins/scripts/deliver.sh'
        input 'Finished using the web site? (Click "Proceed" to continue)'
        sh './jenkins/scripts/kill.sh'
      }
    }
  }
}