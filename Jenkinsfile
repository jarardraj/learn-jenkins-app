pipeline {
    agent any

    stages {
        stage('build') {
            agent{
                docker{
                        image 'node:18-alpine'
                        reuserNode true

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
                '''
            }
        }
    }
}