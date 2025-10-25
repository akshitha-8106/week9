pipeline {
    agent any
    stages {
        stage('Build Docker Image') {
            steps {
                echo 'Building Docker Image...'
                bat 'docker build -t kubedemoapp:v1 .'
            }
        }
        stage('Docker Login') {
            steps {
                bat 'docker login -u bhavani765 -p bhanu@123'
            }
        }
        stage('Push Image to Docker Hub') {
            steps {
                bat 'docker tag kubedemoapp:v1 bhavani765/sample:kubeimage1'
                bat 'docker push bhavani765/sample:kubeimage1'
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f deployment.yaml --validate=false'
                bat 'kubectl apply -f service.yaml'
            }
        }
    }
    post {
        success {
            echo '✅ Pipeline completed successfully!'
        }
        failure {
            echo '❌ Pipeline failed. Check logs.'
        }
    }
}
