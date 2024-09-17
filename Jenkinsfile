pipeline {
    agent any

    stages {
        stage('Build Project') {
            steps {
                git url: 'https://github.com/kolleykalyani/SAproject/', branch: 'master'
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t kalyanikolley/staragileprojectfinance:v1 .'
                    sh 'docker images'
                }
            }
        }

        stage('Docker Login') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh 'docker push kalyanikolley/staragileprojectfinance:v1'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                sh 'sudo docker run -itd --name My-first-container -p 8083:8081 kalyanikolley/staragileprojectfinance:v1'
            }
        }
    }
}
