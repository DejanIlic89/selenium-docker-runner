pipeline{
  agent any
  stages{
    stage("Pull Latest Image"){
      steps{
        bat "docker pull dejan89/selenium-docker"
      }
    }
    stage("Start Grid"){
      steps{
        bat "docker-compose up -d hub chrome firefox"
      }
    }
    stage("Run Test"){
      steps{
        bat "docker-compose up search-module"
      }
    }
  }
  post{
    always{
      script { 
        allure([ 
          includeProperties: false, 
          jdk: '', 
          report: 'target/allure-reports', 
          results: [[path: 'target/allure-results']] 
        ]) 
      }
      archiveArtifacts artifacts: 'output/**'
      bat "docker-compose down"
    }
  }
}
