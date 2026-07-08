pipeline {
    agent any
 
    environment {
        IMAGE_NAME = "my-app"
        CONTAINER_NAME = "my-app-container"
    }
 
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-creds',
                    url: 'https://github.com/rakeshgitdevops/my-app.git'
            }
        }
 
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }
 
        stage('Stop Old Container') {
            steps {
                sh '''
                docker stop $CONTAINER_NAME || true
                docker rm $CONTAINER_NAME || true
                '''
            }
        }
 
        stage('Run New Container') {
            steps {
                sh 'docker run -d --name $CONTAINER_NAME -p 3000:3000 $IMAGE_NAME'
            }
        }
    }
 
    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Build failed.'
        }
    }
}
