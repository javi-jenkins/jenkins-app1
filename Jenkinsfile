pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t app:test .'
            }
        }
        stage('Test') {
            steps {
                echo 'Test'
                sh 'docker run --rm --name app -id -p 80:80 app:test'
                sh '/bin/nc -vz localhost 80'
            }
            post {
                always {
                    sh 'docker stop app'
                }
            }
        }
        stage('Push Registry') {
            steps {
                sh 'docker tag app:test javi1/app:stable'
                sh 'docker push javi1/app:stable'
            }
        }
    }
}
