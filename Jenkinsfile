pipeline {
    agent any

    stages {
        stage('Build and Test') {
            steps {
                echo 'Running Maven clean and package...'
                sh 'mvn clean package'
            }
        }
        
        stage('Dockerize') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t campus-equipment-booking:set-e .'
            }
        }
        
        stage('Deploy to Kubernetes') {
            steps {
                echo 'Applying Kubernetes deployment and service...'
                sh 'kubectl apply -f deployment.yaml'
                sh 'kubectl apply -f service.yaml'
            }
        }
    }
}