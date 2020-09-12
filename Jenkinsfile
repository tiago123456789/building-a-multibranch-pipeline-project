pipeline {
    agent {
        docker {
            image 'node:6-alpine'
            args  '-p 3000:3000'
        }
    }
    environment {
        CI=true
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
 