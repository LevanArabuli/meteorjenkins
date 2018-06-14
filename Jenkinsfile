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
                sh 'apt-get install curl'
                sh 'curl https://install.meteor.com/ | sh'
            }
        }
        stage('Build') {
            steps {
                sh 'meteor npm install'
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
                sh 'cd ./deploy/staging'
                sh 'mup deploy'
            }
        }
    }
}
