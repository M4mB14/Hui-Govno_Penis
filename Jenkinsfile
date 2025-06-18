pipeline {
    agent none
    stages {
        stage('Build') {
            agent {
                label 'fucking-docker' 
            }
            steps {
                echo "Running on docker-agent"
            }
        }
    }
}
