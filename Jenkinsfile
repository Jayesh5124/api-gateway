pipeline {
    agent any 
    tools {
        maven 'my-maven'
        jdk 'my-jdk'
    }
    stages {        
        stage('Clone') {
            steps {
                git url: 'https://github.com/Jayesh5124/api-gateway.git', branch: 'api-gateway'
            }
        }
        stage('Build') {
            steps {
                bat "mvn clean install -DskipTests"
            }
        }
        stage('Test') {
            steps {
                bat "mvn test"
            }
        }
        stage('Deploy') {
            steps { 
                bat "docker rm -f gateway-container"
                bat "docker rmi -f gateway-image"
                bat "docker build -t gateway-image ."
                bat "docker run -p 8060:8060 -d --name gateway-container gateway-image"
            }
        }
    }
}
