pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh 'dotnet build eShopOnWeb.sln'
      }
    }

    stage('test') {
      parallel {
        stage('Unit') {
          steps {
            sh 'dotnet test tests/uniTests'
          }
        }

        stage('integration') {
          steps {
            sh 'dotnet test tests/integrationTests'
          }
        }

        stage('functional') {
          steps {
            sh 'dotnet test tests/functionalTests'
          }
        }

      }
    }

    stage('Deployment') {
      steps {
        sh 'dotnet publish eShopOnWeb.sln -O / var/aspnet'
      }
    }

  }
}