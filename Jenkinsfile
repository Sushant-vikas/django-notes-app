pipeline {
    agent any
    
    stages {
        stage("Code") {
            steps {
                echo "Cloning the code"
                git branch: 'main', url: 'https://github.com/Sushant-vikas/django-notes-app.git'
            }
            
        }
        stage("build") {
            steps {
                echo "Building the image"
                sh "docker build -t my-note-app ."
            }
            
        }
        stage("Push to docker hub") {
            steps {
                echo "Pushing image to docker hub"
                withCredentials([usernamePassword(credentialsId: 'DockerHub', passwordVariable: 'passwordVariable', usernameVariable: 'usernameVariable')]) {
                sh "docker tag my-note-app ${env.usernameVariable}/my-note-app:latest"    
                sh "docker login -u ${env.usernameVariable} -p ${env.passwordVariable}" 
                sh "docker push ${env.usernameVariable}/my-note-app:latest"
                }
                
            }
            
        }
        stage("Deploy") {
            steps {
                echo "Deploying the conatiner"
                //sh "docker run -d -p 8000:8000 sushantvikas007/my-note-app:latest"
                sh "docker-compose down && docker-compose up -d"
            }
            
        }
    }
    
}
