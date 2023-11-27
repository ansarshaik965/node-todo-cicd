pipeline{
    agent any
    
    stages{
        stage("code"){
            steps{
                git url: "https://github.com/ansarshaik965/node-todo-cicd.git", branch: "master"
                echo "Code clone hogaya"
            }
        }
        stage("Build and Test"){
            steps{
                sh "docker build -t node-todo-app ."
                echo "Build bhi hogaya"
            }
        }
        stage("Push to Dockerhub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"DockerHub",passwordVariable:"DockerHubPass",usernameVariable:"DockerHubUser")]){
                sh "docker login -u ${env.DockerHubUser} -p ${env.DockerHubPass}"
                sh "docker tag node-todo-app:latest ${env.DockerHubUser}/node-todo-app:latest"
                sh "docker push ${env.DockerHubUser}/node-todo-app:latest"
                echo "Dockerhub pe push kardiya"
                }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
                echo "Deploy bhi hogaya"
            }
        }
    }
}
