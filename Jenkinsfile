pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/raghunath-jpg/website.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
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
}
