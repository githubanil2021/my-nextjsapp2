pipeline {
    agent any

    environment {
        // Define any environment variables here
        VERCEL_TOKEN = credentials('vercel_token')
    }

    stages {
        stage('Install') {
            steps {
                bat 'npm install'
                // Add your build commands here
            }
        }
       
        stage('Test') {
            steps {
                echo 'Testing...'
                // Add your test commands here
            }
        }
         stage('Build') {
            steps {
                bat 'npm run build'
                // Add your build commands here
            }
        }
        stage('Deploy') {
            steps {
                bat 'npx vercel --prod --yes --token=%VERCEL_TOKEN%'
                // Add your deploy commands here
            }
        }
    }
}