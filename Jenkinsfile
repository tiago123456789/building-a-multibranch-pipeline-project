pipeline {
    agent {
        docker {
            image 'node:10.22-alpine:3.11'
            label 'node'
            args  '-v /tmp:/tmp'
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
        stage('Deploy dev environment') {
             when{
                branch 'development'
            }
            steps {
                input "Continue process?"
                sh './jenkins/scripts/deliver-for-development.sh'
                sh './jenkins/scripts/kill.sh'
            }
        }
         stage('Deploy production environment') {
             when{
                branch 'master'
            }
            steps {
                sh './jenkins/scripts/deliver-for-production.sh'
                sh './jenkins/scripts/kill.sh'
            } 
        }
    }
}
