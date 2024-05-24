pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('e669c344-05a4-4694-84bb-5d55d6ab0c99')
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/jashan-jindal/docker_demo.git', branch: 'master'
            }
        }
        stage('Build') {
            steps {
                script {
                    dockerImage = docker.build("jashanjindal/my-app:${env.BUILD_ID}")
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    dockerImage.inside {
                        sh 'echo "Running tests..."'
                        // Add your test commands here
                    }
                }
            }
        }
        stage('Push') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'e669c344-05a4-4694-84bb-5d55d6ab0c99') {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Deploy your application (e.g., using docker-compose, kubectl, etc.)
                    sh 'echo "Deploying application..."'
                }
            }
        }
    }
}
