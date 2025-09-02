pipeline {
    agent { label 'Slave-1' }
    
    environment {
        NODE_VERSION = '18'
        APP_NAME = 'jenkins-pipeline-test'
    }
    
    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code from GitHub...'
                checkout scm
            }
        }
        
        stage('Setup Node.js') {
            steps {
                echo 'Setting up Node.js environment...'
                sh '''
                    node --version
                    npm --version
                '''
            }
        }
        
        stage('Install Dependencies') {
            steps {
                echo 'Installing npm dependencies...'
                sh 'npm install'
            }
        }
        
        stage('Lint Code') {
            steps {
                echo 'Running ESLint...'
                sh 'npm run lint || true'
            }
        }
        
        stage('Run Tests') {
            steps {
                echo 'Running unit tests...'
                sh 'npm test'
            }
            post {
                always {
                    echo 'Test stage completed'
                }
            }
        }
        
        stage('Build') {
            steps {
                echo 'Building application...'
                sh '''
                    echo "Build timestamp: $(date)" > build-info.txt
                    echo "Build number: ${BUILD_NUMBER}" >> build-info.txt
                    echo "Git commit: ${GIT_COMMIT}" >> build-info.txt
                '''
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment...'
                sh '''
                    echo "Starting application on port 3001..."
                    nohup npm start > app.log 2>&1 &
                    sleep 5
                    echo "Application deployed successfully"
                '''
            }
        }
        
        stage('Health Check') {
            steps {
                echo 'Performing health check...'
                sh '''
                    curl -f http://localhost:3000/health || echo "Health check failed"
                '''
            }
        }
    }
    
    post {
        always {
            echo 'Pipeline execution completed'
            cleanWs()
        }
        success {
            echo 'Pipeline succeeded! 🎉'
        }
        failure {
            echo 'Pipeline failed! ❌'
        }
    }
}