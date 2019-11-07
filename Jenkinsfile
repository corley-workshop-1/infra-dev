pipeline {
    agent none

    stages {
        stage('Setup') {
            agent any
            steps {
                withCredentials([file(credentialsId: 'gpg_key', variable: 'FILE'), string(credentialsId: 'gpg_key_pass', variable: 'GPG_PASS')]) {
                    sh 'echo $GPG_PASS | gpg --batch --import $FILE'
                    sh 'echo $GPG_PASS > key.txt'
                    sh 'touch dummy.txt'
                    sh 'gpg --batch --yes --passphrase-file key.txt --pinentry-mode=loopback -s dummy.txt'
                }
            }
        }
        stage('Deploy in Dev environment') {
            agent any
            steps {
                sh 'sops -i --decrypt db/config.yaml'
                sh 'kubectl version'
                sh 'kubectl apply -f . --recursive'
            }
        }
    }
}
