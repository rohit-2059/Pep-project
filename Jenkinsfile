pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/rohit-2059/Pep-project.git'
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
        sh '''
        sleep 10
        curl http://localhost:3000/health
        '''
    }
}
    }
}