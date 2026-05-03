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
    withCredentials([
      string(credentialsId: 'vercel_token', variable: 'VERCEL_TOKEN'),
      string(credentialsId: 'VERCEL_ORG_ID', variable: 'VERCEL_ORG_ID'),
      string(credentialsId: 'VERCEL_PROJECT_ID', variable: 'VERCEL_PROJECT_ID')
    ]) {
      // set env vars for Vercel CLI
      bat "set VERCEL_ORG_ID=%VERCEL_ORG_ID%"
      bat "set VERCEL_PROJECT_ID=%VERCEL_PROJECT_ID%"

      // clean any old cache
      bat "rmdir /s /q .vercel || exit 0"

      // CI deploy flow
      bat "npx vercel pull --yes --environment=production --token=%VERCEL_TOKEN%"
      bat "npx vercel build --prod --token=%VERCEL_TOKEN%"
      bat "npx vercel deploy --prebuilt --prod --token=%VERCEL_TOKEN%"
    }
  }
}

    }
}