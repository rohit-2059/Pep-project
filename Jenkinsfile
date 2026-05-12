pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git 'YOUR_GITHUB_REPO_URL'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t node-cicd-app .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker rm -f myapp || true

                docker run -d \
                -p 3000:3000 \
                --name myapp \
                node-cicd-app
                '''
            }
        }

        stage('Health Check') {
            steps {
                sh 'curl http://localhost:3000/health'
            }
        }
    }
}