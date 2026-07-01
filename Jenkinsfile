pipeline{
    agent any;
    stages{
            stage("Code"){
            steps{
                git url: "https://github.com/Pradip2602/two-tier-flask-app.git" ,branch: "master"
                echo "Code clone ho gaya..."
            }
        }
        stage("Build"){
            steps{
                sh "docker build -t two-tier-flask-app:latest ."
                echo "Code Build ho gaya..."
            }
        }
        stage("Test"){
            steps{
                echo "Code Test ho gaya..."
            }
        }
        stage("Push To DockerHub"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId: 'dockerHubCreds', 
                    passwordVariable: 'dockerHubPass', 
                    usernameVariable: 'dockerHubUser')]){
                        sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                        echo "Docker login successful...."
                        sh "docker image tag two-tier-flask-app:latest ${env.dockerHubUser}/two-tier-flask-app:latest"
                        sh "docker push ${env.dockerHubUser}/two-tier-flask-app:latest"
                        echo "docker images pushed successfully...."
                    }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker compose up -d"
                echo "Code Deploy ho gaya..."
            }
        }
    }
    
}
