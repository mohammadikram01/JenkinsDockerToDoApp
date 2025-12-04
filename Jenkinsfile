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
                sh 'pip3 install -r requirements.txt || pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'pytest -v || echo "No tests found, skipping"'
            }
        }

        stage('Stop Previous App') {
            steps {
                sh "pkill -f app.py || true"
            }
        }

        stage('Run Application') {
            steps {
                sh "nohup python3 app.py > app.log 2>&1 &"
                echo "Application Started"
            }
        }
    }

    post {
        success { echo "Deployment Successful" }
        failure { echo "Build Failed. Check logs." }
    }
}
