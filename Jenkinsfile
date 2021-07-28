pipeline {
    agent any
    stages {
        stage('Build gradle') {
            steps {
                sh './gradlew build'
            }
        }

        stage('Build docker image') {
            steps {
                sh 'docker build -t repo .'
            }
        }

        stage('login'){
            steps{
                sh 'aws ecr get-login-password --region ap-northeast-2 | docker login --username AWS --password-stdin 776945434852.dkr.ecr.ap-northeast-2.amazonaws.com'
            }
        }

        stage('tag'){
            steps{
                sh 'docker tag repo:latest 776945434852.dkr.ecr.ap-northeast-2.amazonaws.com/repo:latest'
            }
        }

        stage('push'){
            steps{
                sh 'docker push 776945434852.dkr.ecr.ap-northeast-2.amazonaws.com/repo:latest'
            }
        }
    }
}