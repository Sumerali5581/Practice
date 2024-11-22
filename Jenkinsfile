pipeline {
    agent any
  tools{
    python 'Python 3.8'
  }

    stages {
        stage('Clone Repository') {
            steps {
                echo 'Cloning Repository...'
                git branch: 'main', url: 'https://github.com/Sumerali5581/Practice.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Setting up Python environment and installing dependencies...'
                bat 'python -m venv venv'
                bat 'venv\\Scripts\\activate && pip install -r requirements.txt'
            }
        }

        stage('Test Application') {
            steps {
                echo 'Running application tests...'
                bat """
                venv\\Scripts\\activate
                python -m unittest discover -s tests
                """
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                bat "docker build -t my-flask-app ."
            }
        }

        stage('Run Application') {
            steps {
                echo 'Running Docker container...'
                bat "docker run -d -p 5000:5000 my-flask-app"
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed!'
        }
        failure {
            echo 'Pipeline failed. Check logs for errors.'
        }
    }
}
