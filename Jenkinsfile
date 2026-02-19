pipeline {
    agent any

     environment{
        NETLIFY_SITE_ID = ''
        NETLIFY_AUTH_TOKEN = credentials('netlify-token')
     }

    stages {
        stage('build') {
            agent{
                docker{
                        image 'node:18-alpine'
                        reuseNode true

                }
            }
            steps {
                echo 'Hello World'
                sh '''
                    ls -al
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -al
                '''
            }
        }

        stage('test') {
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true

                }
            }

            steps{
                sh '''
                  test -f build/index.html
                   npm test
                  '''
            }
        }

        stage('Deploy') {
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true

                }
            }

            steps{
                sh '''
                    npm install netlify-cli
                    node_modules/.bin/netlify --version
                    echo "Deploying to production . site ID= $NETLIFY_SITE_ID"
                    node_modules/.bin/netlify status

                  '''
            }
        }
    }
    
    post {
        always{
        junit 'test-results/junit.xml'
        }
    }
}