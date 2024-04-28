pipeline {
    agent any
    
    parameters {
        string(name: 'USERNAME', description: 'Username for remote server')
        password(name: 'PASSWORD', description: 'Password for remote server')
        string(name: 'SERVER_DNS', description: 'DNS of the remote server')
        string(name: 'BRANCH_NAME', description: 'Enter git branch name')

    }
    
    stages {
        stage('Git Clone') {
            steps {
                git branch: "${params.BRANCH_NAME}", url: 'https://github.com/chrisdylan237/Demo1.git'

            }
        }
        
        stage('Connect to Remote Server and Copy Files') {
            steps {
                script {
                    // Connect to remote server and copy files
                    sh """
                        scp -r * ${params.USERNAME}@${params.SERVER_DNS}:.
                    """
                }
            }
        }
        
        stage('Check Files on Remote Server') {
            steps {
                script {
                    // SSH to remote server and list files
                    sh """
                        ssh -o StrictHostKeyChecking=no ${params.USERNAME}@${params.SERVER_DNS} 'ls'
                    """
                }
            }
        }
        
        stage('Deploy Application') {
            steps {
                script {
                    // SSH to remote server and deploy application with docker-compose
                    sh """
                        ssh -o StrictHostKeyChecking=no ${params.USERNAME}@${params.SERVER_DNS} 'docker-compose up -d'
                    """
                }
            }
        }
    }
}
