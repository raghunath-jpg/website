pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/raghunath-jpg/website.git'
        BRANCH_NAME = 'main'
    }

    stages {

        stage('Clone') {
            steps {
                script {
                    // Clean workspace before cloning
                    deleteDir()

                    git branch: "${BRANCH_NAME}",
                        url: "${REPO_URL}"
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                npm install
                '''
            }
        }

        stage('Build') {
            steps {
                sh '''
                npm run build
                '''
            }
        }

        stage('Deploy to Nginx') {
            steps {
                sh '''
                sudo rm -rf /var/www/html/*
                sudo cp -r build/* /var/www/html/
                sudo systemctl restart nginx
                '''
            }
        }
    }

    post {
        success {
            echo "Build and Deployment Successful 🚀"
        }
        failure {
            echo "Build Failed ❌ Check Logs"
        }
    }
}
