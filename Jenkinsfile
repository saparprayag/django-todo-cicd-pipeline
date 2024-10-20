@Library("shared") _
pipeline {
    agent { label 'prayag' }
    
    stages {
        stage("Hello") {
            steps {
                script {
                    hello()
                }
            }
        }
        
        stage('Code clone') {
            steps {
                script {
                    url("https://github.com/saparprayag/django-todo-cicd-pipeline.git", "develop")
                }
            }
        }
        
        stage('Build Code') {
            steps {
                script {
                    image("notes-app", "latest", "prayag219")
                }
            }
        }
        
        stage('Scanning the image') {
            steps {
                echo 'Image scanning ho gayi'
            }
        }
        
        stage('Image push to Dockerhub') {
            steps {
                script {
                    dockerhub("notes-app", "latest", "prayag219")
                }
            }
        }
        
        stage('Deploy application') {
            steps {
                script {
                    sh "docker-compose down && docker-compose up -d"
                    echo 'Deployment done'
                }
            }
        }
    }
}
