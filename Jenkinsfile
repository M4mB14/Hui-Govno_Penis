pipeline {
  agent { node {
    label 'agent-docker'
  } }
  stages {
    stage('Test') {
      steps {
        sh '''
            docker ps
        '''
      }
    }
  }
}
