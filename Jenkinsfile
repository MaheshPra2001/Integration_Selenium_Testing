pipeline {
    agent any // Or a specific agent label if needed

    stages {
        stage('Checkout') {
            steps {
                // Checkout the latest code from your Git repository
                git url: 'https://github.com/MaheshPra2001/Integration_Selenium_Testing.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                // Create a virtual environment and install dependencies
                sh 'python3 -m venv venv' 
                sh '. venv/bin/activate && pip install -r requirements.txt' 
            }
        }
        stage('Run Tests') {
            steps {
                // Activate the virtual environment and run tests using pytest
                sh '. venv/bin/activate && pytest --html=report.html --self-contained-html' 
            }
        }
        stage('Publish HTML Report') {
            steps {
                // Publish the generated HTML report
                publishHTML (target: [
                    allowMissing: false,
                    alwaysLinkToLastBuild: false,
                    keepAll: true,
                    reportDir: '.',
                    reportFiles: 'report.html',
                    reportName: 'HTML Report'
                ])
            }
        }
    }
    post {
        always {
            // Cleanup the workspace
            cleanWs() 
        }
        success {
            // Send a notification on successful build
            echo 'Pipeline finished successfully!' 
            // Add notification steps (e.g., email, Slack)
        }
        failure {
            // Send a notification on failed build
            echo 'Pipeline failed!' 
            // Add notification steps (e.g., email, Slack)
        }
    }
}