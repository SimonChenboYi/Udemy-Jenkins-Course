pipeline {
    agent any

    stages {
        // This is a comment

        /*
        multi lines comment
        line
        another line
        */

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
                    ls -la
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
                // Add # in front of sh command to comment out
                sh '''
                    #test -f build/index.html
                    npm test
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
