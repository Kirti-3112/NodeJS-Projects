pipeline {
    agent any

    environment { 
        //NODEJS_HOME = '/usr/local/bin/node'
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
        IMAGE_NAME = "devopskirtihub31/expressweb"
        IMAGE_TAG = "latest"
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

        stage('Build Docker Image') {
            steps {
                dir('02_expressWeb') {
                    echo 'Building Docker Image...'
                    bat 'docker build -t %IMAGE_NAME%:%IMAGE_TAG% .'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                echo 'Pushing Docker Image...'
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                  bat 'docker login -u %USERNAME% -p %PASSWORD%'
                  bat 'docker push %IMAGE_NAME%:%IMAGE_TAG%'
                }    
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying container...'
                script {
                    // Stop any old container
                    bat 'docker stop expresswebapp || exit 0'
                    bat 'docker rm expresswebapp || exit 0'
                    bat "docker run -d -p 3000:3000 --name expresswebapp %IMAGE_NAME%:%IMAGE_TAG%"
                }
            }
        }
    }
}