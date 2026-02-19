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
                    npm --version
                    npm run build
                '''
            }
        }
    }
}