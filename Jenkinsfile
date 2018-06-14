pipeline {
    agent {
        docker {
            image 'ubuntu'
        }
    }
    stages {
        stage('Setup'){
            steps {
                sh 'apt-get update && apt-get -y install curl'
                sh 'apt-get -y install nodejs'
                sh 'apt-get -y install npm'
                sh 'apt-get install -y bsdtar && ln -sf $(which bsdtar) $(which tar)'
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
                sh 'meteor test --allow-superuser --once --driver-package meteortesting:mocha'
            }
        }
        stage('Deploy') {
            when {
                branch 'master'
            }
            steps {
                dir ('cd ./deploy/staging'){
                  sh 'npm install mup'
                  sh 'mup deploy'
                }
            }
        }
    }
}
