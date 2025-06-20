pipeline {
  agent { image 'alpine:latest' }
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
