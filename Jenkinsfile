pipeline {
    agent any
    parameters {
        string defaultValue: 'dylan', name: 'BRANCH_NAME'
        string defaultValue: 'dylan', name: 'IMAGE_NAME'
        string defaultValue: 'dylan', name: 'PORT_NUMBER'
   }
    stages {
        stage('Clone Repository') {
            steps {
                git branch: "${params.BRANCH_NAME}",  
                url: 'https://github.com/chrisdylan237/Demo1.git'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${params.IMAGE_NAME} .'
            }
        }
        
        stage('Deploy Application') {
            steps {
                sh 'docker run -itd -p ${params.PORT_NUMBER}:80 ${params.IMAGE_NAME}'
            }
        }
    }
}
