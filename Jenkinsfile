pipeline {
    agent any

    environment {
        // Set npm cache directory to a writable path
        NPM_CONFIG_CACHE = "${WORKSPACE}/.npm"
        NETLIFY_AUTH_TOKEN = credentials("netlify_token")
        NETLIFY_SITE_ID  = "81ba2f1d-317d-4cc3-bf53-7fdcc9d9c90f"
    }

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                '''
            }
        }
        stage('Test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                 test -f build/index.html
                 npm test
                '''
            }
        }
        stage('Deploy') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                npm install netlify-cli -g
                netlify --version
                netlify deploy --dir=build --prod
                netlify status
                
                '''
            }
        }
    }
    post {
        always {
            junit 'test-results/junit.xml'
            }
    }
}

