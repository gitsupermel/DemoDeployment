pipeline {
    agent any
    
    parameters {
        string(name: 'USERNAME', description: 'Username for remote server')
        string(name: 'PASSWORD', description: 'Password for remote server')
        string(name: 'SERVER_DNS', description: 'DNS of the remote server')
        string(name: 'BRANCH_NAME', description: 'Enter git branch name')
        choice(name: 'DELETE_APPLICATION', choices: ['yes', 'no'], description: 'Delete Docker Compose application?')
    }
    
    stages {
        stage('Git Clone') {
            when {
                expression { params.DELETE_APPLICATION != 'yes' }
            }
            steps {
                git branch: "${params.BRANCH_NAME}", url: 'https://github.com/chrisdylan237/Demo1.git'
            }
        }
        
        stage('Connect to Remote Server and Copy Files') {
            when {
                expression { params.DELETE_APPLICATION != 'yes' }
            }
            steps {
                script {
                    // Connect to remote server and copy files
                    sh "sshpass -p '${params.PASSWORD}' scp -o StrictHostKeyChecking=no -r * ${params.USERNAME}@${params.SERVER_DNS}:."
                }
            }
        }
        
        stage('Check Files on Remote Server') {
            when {
                expression { params.DELETE_APPLICATION != 'yes' }
            }
            steps {
                script {
                    // SSH to remote server and list files
                    sh "sshpass -p '${params.PASSWORD}' ssh -o StrictHostKeyChecking=no ${params.USERNAME}@${params.SERVER_DNS} 'ls'"
                }
            }
        }
        
        stage('Deploy Application') {
            when {
                expression { params.DELETE_APPLICATION != 'yes' }
            }
            steps {
                script {
                    // SSH to remote server and deploy application with docker-compose
                    sh "sshpass -p '${params.PASSWORD}' ssh -o StrictHostKeyChecking=no ${params.USERNAME}@${params.SERVER_DNS} 'sudo docker-compose up -d'"
                }
            }
        }
        
        stage('Delete Application') {
            when {
                expression { params.DELETE_APPLICATION == 'yes' }
            }
            steps {
                script {
                    // SSH to remote server and delete application with docker-compose
                    sh "sshpass -p '${params.PASSWORD}' ssh -o StrictHostKeyChecking=no ${params.USERNAME}@${params.SERVER_DNS} 'sudo docker-compose down --rmi all --volumes --remove-orphans'"
                }
            }
        }
    }
}
