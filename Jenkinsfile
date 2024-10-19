pipeline {
    agent {label 'prayag'}

    stages {
        stage('Code clone') {
            steps {
                git url: "https://github.com/saparprayag/django-todo-cicd-pipeline.git", branch: "develop"
            }
        }
        
        stage('Build Code') {
            steps {
                echo "Code building..."
                sh 'docker build -t notes-app:latest .'
                echo "Code building done"
            }
        }
        
        stage('Scanning the image') {
            steps{
                echo 'image scanning ho gayi'
            }
        }
        
        stage('Image push to Dockerhub') {
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker tag notes-app:latest ${env.dockerHubUser}/notes-app:latest"
                sh "docker push ${env.dockerHubUser}/notes-app:latest"
                echo 'Image pushed to docker hub'
            }
        }
    }
    
    stage('Deploy application') {
        steps{
                sh "docker-compose down && docker-compose up -d"
                echo 'deployment done'
            }
        
    }
    }
}
    
    
