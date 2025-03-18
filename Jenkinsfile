pipeline {
    agent any
    // environment {
    //     NETLIFY_SITE_ID = 'your-site-id'
    //     echo "NETLIFY_SITE_ID: ${NETLIFY_SITE_ID}"
    // }
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
                npm install netlify-cli
                node_modules/.bin/netlify --version
                
                '''
            }
        }
    }
}