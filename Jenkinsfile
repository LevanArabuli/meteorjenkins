pipeline {
    agent {
        docker {
            image 'ubuntu'
        }
    }
    stages {
        stage('Prepare'){
            steps {
                sh 'apt-get update && apt-get -y install curl'
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
