pipeline {
    agent any

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

            steps{
                sh '''
                  test -f build/index.html
                  test -f src/App.js
                  test -f src/App.test.js
                  '''
            }
        }




    }
}