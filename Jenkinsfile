pipeline {
    agent any
 
    stages {
        stage('Build') {
            agent{
                docker{
                    image 'node:20.19-alpine'
                }
            }
            steps {
                sh '''
                test -f build/index.html
                ls -la
                node --version
                npm --version
                npm install
                npm run build
                ls -la
                '''
            }
        }
        stage('Deploy') {
            agent{
                docker{
                    image 'node:20.19-alpine'
                }
            }
            steps {
                sh '''
                npm install netlify-cli -g
                node_modules/.bin/netlify --version
                
                '''
            }
        }
    }
}