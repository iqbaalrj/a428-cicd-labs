pipeline {
    agent {
        docker {
            image 'node:16-buster-slim'
            args '-p 3000:3000'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Manual Approval') {
            steps {
                input message: 'Lanjutkan ke tahap Deploy?'
            }
        }
        stage('Deploy') { 
            steps {
                sh './jenkins/scripts/deliver.sh' 
                sleep time: 1, unit: 'MINUTES'
                input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)' 
                sh './jenkins/scripts/kill.sh' 
            }
        }
    }
}
