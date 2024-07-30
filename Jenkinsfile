pipeline {
    
    agent any
    stages {
        stage('Cloning the code') {
            steps { echo 'Here we are Cloning the code'
                git url : 'https://github.com/XAEA-16/django-todo-cicd.git' , branch: 'develop'
            }
        }
        stage('Building the code') {
            steps { echo 'Here we are building the code'
                sh 'docker build -t django-todo-cici .'
            }
        }
        stage('Pushing the code to Docker Hub') {
            steps { echo 'Here we are pushing the code to Docker Hub'
                withCredentials([usernamePassword(credentialsId: "dockercred", passwordVariable: "dockerhubpass", usernameVariable: "dockerhubuser")]) {
                    sh "docker login --username ${dockerhubuser} --password ${dockerhubpass}"
                    sh "docker tag django-todo-cici ${dockerhubuser}/django-todo-cici:latest"
                    sh "docker push ${dockerhubuser}/django-todo-cici:latest"
                }
            }
        }
        stage('Deployment') {
            steps { echo 'here we are doing the deployment'
             sh "docker compose down && docker compose up -d"
             
             }
        }
    }
}
