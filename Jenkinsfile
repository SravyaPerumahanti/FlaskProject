pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "sravyap1990/flask-app"
    }

    stages {


        stage('Install Dependencies') {
            steps {
                bat 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'pytest'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t flask-app .'
            }
        }

	stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-hub-creds',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    bat '''
                    docker login -u %USER% -p %PASS%
                    docker push %DOCKER_IMAGE%
                    '''
                }
            }
        }

	stage('Deploy to Kubernetes') {
            steps {
	        bat 'set KUBECONFIG=C:\\Users\\Sravya P\\.kube\\config'
                bat 'kubectl apply -f deployment.yaml'
                bat 'kubectl apply -f service.yaml'
            }
        }
    }
}
