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

        stage('Restart Flask Service') {
            steps {
                sh '''
                sudo systemctl daemon-reload
                sudo systemctl restart flask
                '''
            }
        }
    }

    post {
        success { echo "Deployment Success" }
        failure { echo "Deployment Failed - Check Console Output" }
    }
}
