pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }
        stage('Install Dependencies') {
            steps {
                script {
                    sh 'npm install'  // For Unix-based systems
                    bat 'npm install' // For Windows
                }
            }
        }
        stage('Build React App') {
            steps {
                script {
                    sh 'npm run build'  // For Unix-based systems
                    bat 'npm run build' // For Windows
                }
            }
        }
        stage('Deploy to IIS') {
            steps {
                script {
                    // Replace below paths with actual deployment paths
                    bat """
                    xcopy /E /H /Y build\\* C:\\inetpub\\wwwroot\\MyReactApp
                    xcopy /E /H /Y server.js C:\\inetpub\\wwwroot\\MyReactApp
                    """
                }
            }
        }
    }
    post {
        always {
            echo 'Deployment completed.'
        }
    }
}
