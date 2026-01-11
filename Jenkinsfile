pipeline {
    agent any
    environment {
        // Use Jenkins build number to make container & volume names unique
        COMPOSE_PROJECT_NAME = "devops_${BUILD_NUMBER}"
    }
    stages {
        stage('Clone repo') {
            steps {
                git branch: 'main', url: 'https://github.com/Evandro-zigzig/DevOps-Project-Two-Tier-Flask-App.git'
            }
        }
        stage('Build image') {
            steps {
                sh 'docker build -t flask-app .'
            }
        }
        stage('Deploy with docker compose') {
            steps {
                // Bring down any containers from this project (if they exist)
                sh 'docker compose -p $COMPOSE_PROJECT_NAME down -v || true'
                // Start services with dynamic project name, rebuild flask image
                sh 'docker compose -p $COMPOSE_PROJECT_NAME up -d --build'
            }
        }
    }
}
