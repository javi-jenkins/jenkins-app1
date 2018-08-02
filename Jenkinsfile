pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t javi1/app:test .'
            }
        }
        stage('Test') {
            steps {
                echo 'Test'
                sh 'docker run --name app -id -p 80:80 javi1/app:test'
            }
            post {
                always {
                    sh 'docker stop app'
                }
            }
        }
        stage('Push Registry') {
            steps {
                sh 'docker tag javi1/app:test javi1/app:stable'
                sh 'docker push javi1/app:stable'
            }
        }
    }
}
