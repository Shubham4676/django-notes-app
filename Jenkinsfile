pipeline {
    agent any 
    
    stages{
        stage("Cleanup Workspace"){
                steps {
                cleanWs()
                }
        }
        
        stage("Clone-Code"){
            steps {
                echo "Cloning The Code"
                git url:"https://github.com/Shubham4676/django-notes-app.git", branch: "main"
                
            }
            
        }
        stage("Build"){
            steps {
                echo "Building The Code"
                sh "docker build -t shubham4467/my-note-app ."
            }
            
        }
        stage("Push to Docker Hub"){
            steps {
                echo "Pushing the Image to DockerHUb"
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}" 
                sh "docker push shubham4467/my-note-app"
                }
                
            }
            
        }
        stage("Deploy"){
            steps {
                echo "Deploying The Container"
                sh "docker-compose down && docker-compose up -d"
            }
             
        }
    }
}
