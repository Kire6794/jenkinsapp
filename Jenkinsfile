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
                sh '''
                # npm install netlify-cli
                # node_modules/.bin/netlify --version
                # echo "Deploying to Site ID: $NETLIFY_SITE_ID"
                # node_modules/.bin/netlify status
                # node_modules/.bin/netlify deploy --prod --dir=build
                
                #### custom docker image
                #netlify --version
                #echo "Deploying to Site ID: $NETLIFY_SITE_ID"
                #netlify status
                #netlify deploy --prod --dir=build

                #### custom AWS image
                aws --version

                '''
            }
        }
    }
}