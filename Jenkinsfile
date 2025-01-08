pipeline {
    agent any
    tools {
        nodejs 'Node23.6' // Ensure Node23.6 is configured in Jenkins
    }
    stages {
        stage('Installing Dependencies') {
            steps {
                script {
                    // Install dependencies with npm
                    sh '''
                        npm install --no-audit
                        node -v
                        npm -v
                    '''
                }
            }
        }
    }
}

