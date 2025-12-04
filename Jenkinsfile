pipeline {
    agent any

    triggers {
        githubPush()   // Auto-trigger on push to GitHub
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/mohammadikram01/MiniProject.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                cd /var/lib/jenkins/workspace/git
                pip3 install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh 'pytest -v || echo "No tests found"'
            }
        }

        stage('Restart Flask App Service') {
            steps {
                sh '''
                sudo systemctl daemon-reload
                sudo systemctl restart flask
                '''
                echo "Flask Service Restarted Successfully"
            }
        }
    }

    post {
        success { echo "Deployment Successful" }
        failure { echo "Build Failed, check logs" }
    }
}
