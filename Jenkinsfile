pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                script {
                    docker.build("my-http-python-app")
                }
            }
        }
        
        stage('Test') {
            steps {
                script {
                    docker.image("my-http-python-app").inside {
                        sh 'python -m unittest discover'
                    }
                }
            }
        }
        stage('Dockerize') {
            steps {
                sh 'docker build -t my-http-python-app .'
            }
        }
    }
    
    post {
        success {
            sh 'docker run -p 8080:80 my-http-python-app'
        }
    }
}
