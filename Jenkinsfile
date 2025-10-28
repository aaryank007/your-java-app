pipeline {
    agent any

    tools {
        maven 'Maven3'
        jdk 'JDK17'
    }

    stages {
        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t hello-app .'
            }
        }

        stage('Run Container') {
            steps {
                bat 'docker run hello-app'
            }
        }
    }
}
