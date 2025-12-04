DevOps Project – Flask Todo App CI/CD with Jenkins & Docker

This project demonstrates a simple CI/CD pipeline where a Flask To-Do application automatically builds and deploys as a Docker container on AWS EC2 whenever code is pushed to GitHub.

Tech Used

Python + Flask
Docker
Jenkins (CI/CD)
GitHub Webhook
AWS EC2

📁 Structure
MiniProject/
│── app.py
│── requirements.txt
│── Dockerfile
│── Jenkinsfile
└── templates/index.html

Jenkins Pipeline (Summary)

Pull code from GitHub on every push

Install dependencies

Build Docker image

Stop old container & deploy new one

docker build -t mini-flask-app .

docker stop mini-flask-app || true

docker rm mini-flask-app || true

docker run -d -p 50001:5000 --name mini-flask-app mini-flask-app

Run App
http://<EC2-IP>:50001


Example:

http://54.226.154.186:50001

Outcomes

Fully automated CI/CD pipeline

Auto deployment on every git push

Application containerized with Docker
