pipeline {
    agent { label 'linux' }
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }
    environment {
        DOCKERHUB_CREDENTIALS = credentials('kkeska-dockerhub')
    }
    stages {
        stage('Build') {
            steps {
              sh 'docker build -t kkeska/lab1:latest .'
            }
        }
        stage('Login') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Push') {
            steps {
                sh 'docker push kkeska/lab1:latest'
            }
        }
    }
    post {
        always {
            sh 'docker logout'
        }
    }
}