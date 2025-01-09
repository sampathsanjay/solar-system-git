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
        stage('Security Checks') {
            parallel {
                stage('NPM Dependency Audit') {
                    steps {
                        script {
                            // Audit npm dependencies for critical issues
                            sh '''
                                npm audit --audit-level=critical
                            '''
                        }
                    }
                }
                stage('OWASP Dependency Check') {
                    steps {
                        script {
                            dependencyCheck additionalArguments: '''
                                --scan ./ 
                                --out ./ 
                                --format ALL 
                                --prettyPrint
                            ''', odcInstallation: 'OWASP-DependencyCheck10'

                            publishHTML([
                                allowMissing: true, 
                                alwaysLinkToLastBuild: true, 
                                keepAll: true, 
                                reportDir: './', 
                                reportFiles: 'dependency-check-report.html', 
                                reportName: 'Dependency Check Report', 
                                reportTitles: ''
                            ])
                        }
                    }
                }
            }
        }
    }
}

