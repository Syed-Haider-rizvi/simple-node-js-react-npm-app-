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
                    // Check the operating system and run the corresponding command
                    if (isUnix()) {
                        sh 'npm install'  // For Unix-based systems
                    } else {
                        bat 'npm install' // For Windows
                    }
                }
            }
        }

        stage('Build React App') {
            steps {
                script {
                    // Check the operating system and run the corresponding build command
                    if (isUnix()) {
                        sh 'npm run build'  // For Unix-based systems
                    } else {
                        bat 'npm run build' // For Windows
                    }
                }
            }
        }

        stage('Deploy to IIS') {
            steps {
                script {
                    // Windows deployment using bat commands
                    if (isUnix()) {
                        echo "Deploying to IIS is not supported on Unix-based systems"
                    } else {
                        bat """
                        REM Copy React build files to the IIS root directory
                        xcopy /E /H /Y build\\* C:\\inetpub\\wwwroot\\MyReactApp
                        
                        REM Copy files from network share (assuming the network path is valid)
                        xcopy /E /H /Y \\\\172.16.14.79\\MyReactApp\\* C:\\inetpub\\wwwroot\\MyReactApp
                        """
                    }
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
