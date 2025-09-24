pipeline {
    agent any

    stages {
        stage('Connect to GitHub') {
            steps {
                echo 'Checking out...'
                // Add your build steps here
                checkout scmGit(
                    branches: [[name: '*/main']], 
                    extensions: [], 
                    userRemoteConfigs: [[url: 'https://github.com/SamuelEzra/jenkins-pipeline.git']]
                )
            }
        }
        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                script {
                    sh 'docker build -t ez-jenkins .'
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                echo 'Running Docker container...'
                script {
                    sh 'docker run -d -p 8081:80 ez-jenkins'
                }
                // Add your deploy steps here
            }
        }
    }

    post {
        always {
            echo 'This will always run after the stages.'
        }
        success {
            echo 'This will run only if the pipeline succeeds.'
        }
        failure {
            echo 'This will run only if the pipeline fails.'
        }
    }
}