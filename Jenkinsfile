pipeline {
  agent { node {
    label 'agent-docker'
  } }
  stages {
    stage('Test') {
      steps {
        sh '''
            echo "Hello from Docker!"
        '''
      }
    }
  }
}
