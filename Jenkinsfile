pipeline {
    agent any

    tools {
        jdk 'JDK17'
        maven 'Maven_3'
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
