pipeline {
    agent any

    stages {
        stage('Cloning Git repository') {
            steps {
                git branch: 'main', url: 'https://github.com/ozysouza/jk-public-gh.git'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t webapp:${BUILD_NUMBER} .'
            }
        }

        stage('Application deploy') {
            steps {
                sh '''
                docker stop webapp_ctr -t 0
                docker run --rm -d -p 3000:3000 --name webapp_ctr webapp:${BUILD_NUMBER}
                '''
            }
        }
    }
    
}
