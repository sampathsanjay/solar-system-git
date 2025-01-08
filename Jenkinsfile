pipeline {
    agent any
    tools {
        nodejs 'Node23.6'
    }
    stages {
        stage('Check Node.js Version') {
            steps {
                script {
                    // Running the node command to check the version
                    sh '''
                       node -v
                       npm -v
                    '''
                }
            }
        }
    }
}

