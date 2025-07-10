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
                    bat 'npm install'
                }
            }
        }

        stage('Lint') {
            steps {
                dir('02_expressWeb') {
                    echo 'Running lint...'
                    bat 'npm run lint || true'
                }
            }
        }

        stage('Start App') {
            steps {
                dir('02_expressWeb') {
                    bat 'npm start &'
                }
            }
        }
    }
}