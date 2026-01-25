pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Docker Build') {
            steps {
                dir('githubjenkins/githubjenkins') {
                   // 1. Build the image (No -d here)
            sh "docker build -t my-dotnet-app:latest ."
            
            // 2. Stop and remove the old container if it exists (so it doesn't conflict)
            sh "docker stop my-container || true && docker rm my-container || true"
            
            // 3. Run the NEW image in detached mode (-d)
            sh "docker run -d --name my-container -p 8085:8080 my-dotnet-app:latest"
                }
            }
        }
        stage('Ansible Deploy') {
            steps {
                dir('githubjenkins/githubjenkins') {
                    sh "ansible-playbook -i hosts.ini deploy.yml"
                }
            }
        }
    }
}
