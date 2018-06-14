pipeline {
    agent {
        docker {
            image 'node:6-alpine'
            args '-p 3000:3000'
        }
    }
    stages {
        stage('Prepare'){
            steps {
                sh 'curl https://install.meteor.com/ | sh'
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh 'meteor test --once --driver-package meteortesting:mocha'
            }
        }
        stage('Deploy') {
            when {
                branch 'master'
            }
            steps {
                sh 'npm install --global mup'
            }
        }
    }
}
