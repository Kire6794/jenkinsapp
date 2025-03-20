pipeline {
    agent any
    // environment {
    //     NETLIFY_SITE_ID = 'your-site-id'
    //     echo "NETLIFY_SITE_ID: ${NETLIFY_SITE_ID}"
    // }
    stages {
        // stage('Docker'){
        //     steps{
        //         sh 'docker build -t my-docker-image .'
        //     }
        // }
        // stage('Build') {
        //     agent{
        //         docker{
        //             image 'node:20.19-alpine'
        //         }
        //     }
        //     steps {
        //         sh '''
        //         test -f build/index.html
        //         ls -la
        //         node --version
        //         npm --version
        //         npm install
        //         npm run build
        //         ls -la
        //         '''
        //     }
        // }
        stage('Deploy AWS') {
            agent{
                docker{
                    //image 'node:20.19-alpine'
                    image 'amazon/aws-cli'
                }
            }
            steps {
                withCredentials([usernamePassword(credentialsId: 'my-aws-jenkins', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')])
                {
                    sh '''
                    aws --version
                    aws s3 ls
                    '''
                }
            }
        }
        
    }
}