pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Abdallah-Abdelnour/jenkins-projet.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t monsite:latest .'
            }
        }

        stage('Test') {
            steps {
                echo "Vérification basique des fichiers HTML/CSS/JS"
                sh 'ls -l'
            }
        }

        stage('Push to Registry') {
            steps {
                echo "Push sur Docker Hub (on fera la config plus tard)"
            }
        }
/*
        stage('Deploy to AWS') {
            steps {
                sshagent(['AWS_KEY']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no ubuntu@IP_AWS "docker stop monsite || true"
                    ssh ubuntu@IP_AWS "docker rm monsite || true"
                    ssh ubuntu@IP_AWS "docker run -d -p 80:80 --name monsite monsite:latest"
                    '''
                }
            }
        }*/
    }
}
