pipeline {
    agent any

    environment {
        DB_PASSWORD = credentials('db-password')
        JWT_SECRET = credentials('jwt-secret')
        MYSQL_ROOT_PASSWORD = credentials('mysql-root-password')
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out BusBooking source code'
                checkout scm
            }
        }

        stage('Validate Docker Compose') {
            steps {
                bat 'docker compose config --quiet'
            }
        }

        stage('Build Docker Images') {
            steps {
                bat 'docker compose build'
            }
        }

        stage('Check Docker Images') {
            steps {
                bat 'docker images'
            }
        }
    }

    post {
        success {
            echo 'BusBooking CI pipeline completed successfully!'
        }
        failure {
            echo 'BusBooking CI pipeline failed. Check the console output.'
        }
    }
}