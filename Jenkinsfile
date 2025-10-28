pipeline {
  agent any
  environment {
    DOCKERHUB_CREDENTIALS = 'dockerhub-creds'  // Jenkins credentials ID
    IMAGE_NAME = 'yourdockerhubusername/java-app'
  }
  stages {
    stage('Checkout') {
      steps { checkout scm }
    }
    stage('Build') {
      steps { sh './mvnw clean package -DskipTests' } // or 'mvn'
    }
    stage('Test') {
      steps { sh './mvnw test' }
    }
    stage('Build Docker Image') {
      steps {
        script {
          dockerImage = docker.build("${IMAGE_NAME}:${BUILD_NUMBER}")
        }
      }
    }
    stage('Push Image') {
      steps {
        script {
          docker.withRegistry('https://index.docker.io/v1/', DOCKERHUB_CREDENTIALS) {
            dockerImage.push()
            dockerImage.push('latest')
          }
        }
      }
    }
    stage('Run Container') {
      steps {
        sh "docker run -d --rm -p 8080:8080 ${IMAGE_NAME}:${BUILD_NUMBER}"
      }
    }
  }
  post {
    always { cleanWs() }
  }
}
