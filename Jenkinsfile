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
        stage('Deploy AWS') {
            agent{
                docker{
                    //image 'node:20.19-alpine'
                    image 'amazon/aws-cli'
                    reuseNode true
                    args '--entrypoint=""'
                }
            }
            environment{
                AWS_S3_BUCKET = 'my-new-jenkins-2025320'
            }
            steps {
                withCredentials([usernamePassword(credentialsId: 'my-aws-jenkins', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')])
                {
                    sh '''
                        aws --version
                        aws s3 ls
                        # echo "Hello S3!" > index.html
                        # aws s3 cp index.html s3://my-new-jenkins-2025320/index.html
                        aws s3 sync build s3://$AWS_S3_BUCKET
                    '''
                }
            }
        }
    }
}