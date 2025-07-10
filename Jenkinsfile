pipeline {
    agent any

    environment { 
        NODEJS_HOME = '/usr/local/bin/node'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning repo...'
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                dir('02_expressWeb') {
                    echo 'Installing dependencies...'
                    sh 'npm install'
                }
            }
        }

        stage('Lint') {
            steps {
                dir('02_expressWeb') {
                    echo 'Running lint...'
                    sh 'npm run lint || true'
                }
            }
        }

        stage('Start App') {
            steps {
                dir('02_expressWeb') {
                    sh 'npm start &'
                }
            }
        }
    }
}