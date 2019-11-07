pipeline {
    agent none

    stage('Deploy in Dev environment') {
            agent any
            steps {
                sh 'kubectl version'
                sh 'kubectl apply -f . --recursive'
            }
        }
    }
}
