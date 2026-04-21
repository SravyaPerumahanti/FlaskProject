pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/SravyaPerumahanti/FlaskProject.git'
            }
        }

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
    }
}
