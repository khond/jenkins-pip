pipeline {
    agent any

    environment {
        // Set npm cache directory to a writable path
        NPM_CONFIG_CACHE = "${WORKSPACE}/.npm"
        NETLIFY_AUTH_TOKEN = credentials("netlify_token")
    }

    stages {
        /*stage('Build') {
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
        }*/
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
                echo $NETLIFY_AUTH_TOKEN
                netlify sites:list
                '''
            }
        }
    }
    //post {
        //always {
            //junit 'test-results/junit.xml'
            //}
    //}
}

