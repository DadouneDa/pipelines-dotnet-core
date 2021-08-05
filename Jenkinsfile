pipeline {
  agent {
    node {
      label 'centos7'
    }

  }
  stages {
    stage('Checkout_git') {
      steps {
        git(url: 'https://github.com/DadouneDa/pipelines-dotnet-core.git', branch: 'master', changelog: true, poll: true, credentialsId: 'dd_github')
      }
    }

    stage('Build') {
      steps {
        sh 'dotnet build'
      }
    }

    stage('Run') {
      steps {
        sh 'dotnet run'
      }
    }

    stage('Kill_App') {
      steps {
        sh 'pkill -f node'
      }
    }

    stage('Package') {
      steps {
        sh 'dotnet publish'
      }
    }

  }
}