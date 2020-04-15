pipeline{
  agent any
  stages{
    stage("Start Grid"){
      steps{
        sh "docker-compose up -d Hub Chrome Firefox"
      }
    }
    stage("Run Test"){
      steps{
        sh "docker-compose up search-module book-flight-module"
      }
    }
    stage("Stop Grid"){
      steps{
        sh "docker-compose down"
      }
    }
  }
}
