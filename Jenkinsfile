pipeline {
  agent any

  tools {
    jdk 'jdk21'
  }

  environment {
    SONAR_HOST_URL = 'http://192.168.50.4:9000'
  }

  stages {
    stage('Checkout') {
      steps { checkout scm }
    }

    stage('Build') {
      steps {
        sh 'chmod +x mvnw || true'
        sh './mvnw -B -DskipTests clean package'
      }
    }

    stage('SonarQube') {
      steps {
        withCredentials([string(credentialsId: 'sonarcube', variable: 'SONAR_AUTH_TOKEN')]) {
          sh "./mvnw -B sonar:sonar -Dsonar.projectKey=devops_git -Dsonar.host.url=${SONAR_HOST_URL} -Dsonar.token=${SONAR_AUTH_TOKEN}"
        }
      }
    }

    stage('Archive') {
      steps {
        archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
      }
    }
  }
}
