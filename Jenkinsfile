pipeline {
    agent any
    environment{
        AWS_DEFAULT_REGION = 'us-east-2'
    }
    stages {
        stage('Build') {
            agent{
                docker{
                    image 'node:20.19-alpine'
                }
            }
            steps {
                sh '''
                ls -la
                node --version
                npm --version
                npm install
                npm run build
                ls -la
                '''
            }
        }
        // stage('Test') {
        //     agent {
        //         docker {
        //             image 'node:22-alpine'
        //             reuseNode true
        //         }
        //     }

        //     steps {
        //         sh '''
        //             test -f build/index.html
        //             npm test
        //         '''
        //     }
        // }
        stage('Deploy AWS') {
            agent{
                docker{
                    image 'amazon/aws-cli'
                    reuseNode true
                    args 'root --entrypoint=""'
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
                        yum install jq -y

                        LATEST_TD_REVISION=$(aws ecs register-task-definition --cli-input-json file://task-definition.json | jq '.taskDefinition.revision')
                        aws ecs update-service --cluster my-react-cluster-Prod-EM --service MyReactApp-Service-Prod --task-definition Temp-TaskDefinition-Prod:$LATEST_TD_REVISION
                    '''
                }
            }
        }
    }
}