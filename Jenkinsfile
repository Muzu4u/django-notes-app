pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                echo 'Cloning code from github'
                git branch: 'main', credentialsId: 'bec8131d-8434-4974-82c0-0b204b0bac25', url: 'https://github.com/Muzu4u/django-notes-app.git'
            }
        }
        stage('Build Project') {
            steps {
                echo 'Building Image'
                sh 'docker build -t mynotes-app .'
            }
        }
        
        stage('Testing Image') {
            steps {
                script{
                echo 'Testing Image'
                def imageExists = sh(script: "docker inspect -f '{{.Id}}' mynotes-app:latest", returnStatus: true)
                    if (imageExists == 0) {
                        echo 'Test passed: Image mynotes-app:latest exists'
                    } else {
                        echo 'Test failed: Image mynotes-app:latest does not exist'
                    }
                }
            }
        }
        
        stage('Deploying Project') {
            steps {
                echo 'Deploying Project'
                sh 'docker run -d -p 8000:8000 mynotes-app'
            }
        }
    }
}

