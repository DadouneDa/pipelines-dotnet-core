pipeline {
  agent {
    node {
      label 'centos7'
    }

  }
  stages {
    stage('Checkout_git') {
      steps {
        cleanWs()
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
        sh 'dotnet run &'
      }
    }

    stage('Kill_App') {
      steps {
        //sh 'pkill -f node'
        sh 'killall dotnet'
      }
    }

    stage('Package') {
      steps {
        sh 'dotnet publish'
        sh 'zip -r package.zip .'
        archiveArtifacts(artifacts: 'package.zip', onlyIfSuccessful: true)
        cleanWs(cleanWhenSuccess: true)
        slackSend(channel: 'dd_devops', color: '#3EA652', message: "Success: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
      }
    }

  }
}
