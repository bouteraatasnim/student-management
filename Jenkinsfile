pipeline {
  agent any

  tools {
    jdk 'jdk17'
  }

  environment {
    MVN = "./mvnw"
  }

  stages {
    stage('Checkout') {
      steps { checkout scm }
    }

    stage('Build') {
      steps {
        sh 'chmod +x mvnw || true'
        sh '${MVN} -B -DskipTests clean package'
      }
    }

    stage('Archive') {
      steps {
        archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
      }
    }
  }
}
