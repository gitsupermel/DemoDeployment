pipeline {
    agent any

    stages {
        stage('Update System') {
            steps {
                // Add your steps to update the system here
                sh 'echo "Updating system..."'
            }
        }
        stage('Create Folder: Dylan') {
            steps {
                script {
                    // Create a folder named 'dylan'
                    dir('dylan') {
                        sh 'mkdir dylan'
                        echo 'Folder "dylan" created'
                    }
                }
            }
        }
        stage('Create Folder: Chris') {
            steps {
                script {
                    // Create a folder named 'chris'
                    dir('chris') {
                        sh 'mkdir chris'
                        echo 'Folder "chris" created'
                    }
                }
            }
        }
    }
}
