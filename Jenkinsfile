pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/raghunath-jpg/website.git'
        BRANCH_NAME = 'main'
    }

    stages {

        stage('Clone') {
            steps {
                deleteDir()
                git branch: "${BRANCH_NAME}",
                    url: "${REPO_URL}"
            }
        }

        stage('Deploy to Nginx') {
            steps {
                sh '''
                sudo rm -rf /var/www/html/*
                sudo cp -r * /var/www/html/
                sudo systemctl restart nginx
                '''
            }
        }
    }

    post {
        success {
            echo "Deployment Successful 🚀"
        }
        failure {
            echo "Build Failed ❌"
        }
    }
}
