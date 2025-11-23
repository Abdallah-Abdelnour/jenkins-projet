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

         stage('Push to Docker Hub') {
            steps {
                 withCredentials([usernamePassword(credentialsId: 'docker-password', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                    echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin

                    # Tag version unique
                    docker tag monsite:latest $DOCKER_USER/monsite:${BUILD_NUMBER}
                    docker tag monsite:latest $DOCKER_USER/monsite:latest

                    # Push
                    docker push $DOCKER_USER/monsite:${BUILD_NUMBER}
                    docker push $DOCKER_USER/monsite:latest
                    '''
                }
            }
        }

        stage('Deploy to AWS (Staging)') {
            steps {
                sshagent(['AWS_KEY']) {
                    withCredentials([usernamePassword(credentialsId: 'docker-password', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh '''
                        ssh -o StrictHostKeyChecking=no ubuntu@16.171.114.44 "
                            echo \\"$DOCKER_PASS\\" | docker login -u \\"$DOCKER_USER\\" --password-stdin &&
                            docker pull $DOCKER_USER/monsite:latest &&
                            docker stop monsite || true &&
                            docker rm monsite || true &&
                            docker run -d -p 80:80 --name monsite $DOCKER_USER/monsite:latest
                        "
                        '''
                    }
                }
            }
        }


/* --> 

khas nezidlah bach ye dir push f docker hub mais avant u supprime ay whda andha le meme nom 
moraha yetala3eha 
nebda cd pipline b aws 
----------------------------

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
        }
*/
    }
}