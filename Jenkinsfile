pipeline {
    agent any

    tools {
        maven 'Maven By Jenkin'
    }

    environment {
        APP_NAME = "springboot-demo"
        IMAGE_TAG = "1.0"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/jayeshjaiswal-developer/SpringWebApp2.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                echo 'Tests skipped for demo'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t $APP_NAME:$IMAGE_TAG .'
            }
        }

        stage('Docker Run') {
            steps {
                sh '''
                   docker stop $APP_NAME || true
                   docker rm $APP_NAME || true
                   docker run -d -p 9091:8080 --name $APP_NAME $APP_NAME:$IMAGE_TAG
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully'
        }
        failure {
            echo 'Pipeline failed'
        }
        always {
            echo 'Pipeline finished'
        }
    }
}
