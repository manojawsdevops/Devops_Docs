pipeline {
  agent any
  stages {
    stage('Log Ant version info') {
      steps {
        sh 'ant -version'
      }
    }
    stage('GitHub Jenkins Ant Build') {
      steps {
        git 'https://github.com/learn-devops-fast/rps-ant.git'
        sh 'ant clean compile test package war'
      }
    }
  }
}
