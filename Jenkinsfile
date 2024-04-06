pipeline {
    agent {
        docker {
            image 'node:lts-buster-slim'
            args '-p 3000:3000'
        }
    }
    environment {
        CI = 'true'
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
        stage('Manual Approve'){
            steps{
                input message: 'Lanjut ke tahap Deploy? (klik "Proceed" untuk melanjutkan atau "Abort" untuk menghentikan)'
            }
        }
        stage('Deploy') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                input message: 'Sudah selesai menggunakan React App? (klik "Proceed" untuk mengakhiri)'
                sh './jenkins/scripts/kill.sh'
                sleep(60)
            }
        }
    }
}