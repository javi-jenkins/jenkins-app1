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
                withCredentials([usernamePassword(credentialsId: 'Docker-Hub', passwordVariable: 'Docker-HubPassword', usernameVariable: 'Docker-HubUser')]) {
          sh 'docker login -u ${env.Docker-HubUser} -p ${env.Docker-HubPassword}'
                sh 'docker push javi1/app:stable'
                }  
            }
        }
    }
}
