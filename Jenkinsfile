pipeline {
    agent none

    stages {
        stage('Deploy in Dev environment') {
            agent any
            steps {
                sh 'kubectl version'
                sh 'kubectl apply -f . --recursive'
            }
        }
    }
}
