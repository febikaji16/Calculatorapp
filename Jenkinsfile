pipeline {
  agent any
  tools { maven 'M3' JDK 'JDK17' }
  stages {
    stage('Checkout') { 
      steps { 
        git branch: 'main', url: 'https://github.com/febikaji16/Calculatorapp.git'
      } 
    }
    stage('Build & Test') {
      steps {
        bat 'mvn -B -e -DskipTests=false clean verify'
      }
      post {
        always {
          junit 'target/surefire-reports/*.xml'
          archiveArtifacts artifacts: 'target/*.jar', fingerprint: true, onlyIfSuccessful: false
        }
      }
    }
    stage('Run') {
      when { expression { return isUnix() == false } }
      steps {
        bat 'mvn -q exec:java'
      }
    }
  }
}
