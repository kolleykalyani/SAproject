pipeline {
    agent any
    stages{
        stage('build project'){
            steps{
                git url:'https://github.com/kolleykalyani/SAproject/', branch: "master"
                sh 'mvn clean package'
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t kalyanikolley/staragileprojectfinance:v1 .'
                    sh 'docker images'
                }
            }
        }
        stage('docker login'){
           steps{
                withcredentials([usernamepassword(credentialsId: 'dockerhub-pwd',passwordvariable: 'PASS',usernamevariable: 'USER')])
                   sh "echo $pass | docker login -u $user --password-stdin"
                   sh 'docker push kalyanikolley/staragileprojectfinance:v1'
                }
            }
         }
        
     stage('Deploy') {
            steps {
                sh 'sudo docker run -itd --name My-first-containe21211 -p 8083:8081 kalyanikolley/staragileprojectfinance:v1'
                  
                }
            }
        
    }
}
