pipeline {
  agent { node {
    label 'agent2'
  } }
  stages {
    stage('Test') {
      steps {
        sh '''
            ansible --version && \
            terraform --version && \
            docker --version
        '''
      }
    }
  }
}
