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
                    sh "docker build -t my-dotnet-app:latest ."
                }
            }
        }
        stage('Ansible Deploy') {
            steps {
                dir('githubjenkins/githubjenkins') {
                    sh "ansible-playbook deploy.yml"
                }
            }
        }
    }
}
