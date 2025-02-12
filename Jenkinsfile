pipeline {
    agent any

    environment {
        BOT_TOKEN = credentials('telegram-bot-token')
    }

    stages {
        stage('Initialize') {
            steps {
                script {
                    sh 'make venv && make install'
                }
            }
        }
            
        stage('Inject Env') {
            steps {
                script {
                    withCredentials([file(credentialsId: 'tbot-env-file', variable: 'ENV_FILE')]){
                        sh "cat $ENV_FILE >> .env"
                    }
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'make build'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sh 'make deploy'
                }
            }
        }
    }

    post {
        always {
            echo 'This will always run'
        }
    }
}
