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
      archiveArtifacts artifacts: 'output/**'
      bat "docker-compose down"
      script { 
        allure([ 
          includeProperties: false, 
          jdk: '', 
          properties: [[key: 'allure.results.directory', value: 'target/allure-results']], 
          reportBuildPolicy: 'ALWAYS', 
          report: 'target/allure-reports', 
          results: [[path: 'target/allure-results']] 
        ]) 
      }
    }
  }
}
