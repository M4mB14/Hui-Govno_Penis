pipeline {
  agent { node {
    label 'agent2'
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
