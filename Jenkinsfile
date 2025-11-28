pipeline {
    agent any

    environment {
        VERCEL_TOKEN = credentials('vercel_token')
    }

    stages {
        stage('Instalar dependencias de frontend') {
            agent {
                docker {
                    image 'node:18-alpine'
                }
            }

            steps {
                sh 'npm install'
            }
        }

        stage('Construir proyecto frontend') {
            agent {
                docker {
                    image 'node:18-alpine'
                }
            }

            steps {
                sh 'npm run build'
            }
        }

        stage('Deploy hacia vercel...') {
            agent {
                docker {
                    image 'node:18-alpine'
                    args '-u root'
                }
            }

            steps {
                sh """
                    apk add --no-cache bash
                    npm install -g vercel
                    vercel deploy --prod --name front-vercel --token $VERCEL_TOKEN --yes
                """
            }
        }


    }
}