pipeline {
    agent { label 'windows' }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/santosh-github-devops/website.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat '''
                echo Building Docker Image...
                docker build -t html-app .
                '''
            }
        }

        stage('Stop & Remove Old Container') {
            steps {
                bat '''
                echo Stopping and removing old container if exists...
                docker rm -f html-container >nul 2>&1 || exit 0
                '''
            }
        }

        stage('Run New Container') {
            steps {
                bat '''
                echo Starting new container...
                docker run -d -p 4040:80 --name html-container html-app
                echo Deployment successful.
                '''
            }
        }

    }
}