pipeline {
    agent any

    triggers {
        githubPush()
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/mohammadikram01/MiniProject.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                cd /var/lib/jenkins/workspace/git
                docker build -t mini-flask-app .
                '''
            }
        }

        stage('Stop Old Container') {
            steps {
                sh "docker stop mini-flask-app || true"
                sh "docker rm mini-flask-app || true"
            }
        }

        stage('Run New Container') {
            steps {
                sh '''
                cd /var/lib/jenkins/workspace/git
                docker run -d --name mini-flask-app -p 5001:5000 mini-flask-app
                '''
            }
        }
    }

    post {
        success { echo "Docker Deployment Successful" }
        failure { echo "Docker Deployment Failed" }
    }
}
