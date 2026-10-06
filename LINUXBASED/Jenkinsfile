pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/santosh-github-devops/website.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                echo "Building Docker Image..."
                docker build -t html-app .
                '''
            }
        }

        stage('Stop & Remove Old Container') {
            steps {
                sh '''
                echo "Checking if container exists..."

                if docker ps -a --format '{{.Names}}' | grep -w html-container > /dev/null; then
                    echo "Container exists. Stopping..."
                    docker stop html-container
                    docker rm html-container
                    echo "Old container removed."
                else
                    echo "No old container found."
                fi
                '''
            }
        }

        stage('Run New Container') {
            steps {
                sh '''
                echo "Starting new container..."
                docker run -d -p 4040:80 --name html-container html-app
                echo "Deployment successful."
                '''
            }
        }

    }
}