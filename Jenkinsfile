pipeline{
    agent any
    
    environment {
        dotnet ='C:\\Program Files (x86)\\dotnet\\'
        }
        
    triggers {
        pollSCM 'H * * * *'
    }
    stages{
      stage('Checkout') {
        steps {
          git url: 'https://github.com/Inspyro/jenkinstest', branch: 'master'
        }
      }
      stage('Restore packages'){
        steps{
          bat "dotnet restore Calculator\\Calculator.csproj"
        }
      }
      stage('Clean'){
        steps{
          bat "dotnet clean Calculator\\Calculator.csproj"
        }
      }
      stage('Build'){
        steps{
          bat "dotnet build Calculator\\Calculator.csproj --configuration Release"
        }
      }
      stage('Publish'){
        steps{
          bat "dotnet publish Calculator\\Calculator.csproj "
        }
      }
    }
    post{
      always{
        emailext body: "${currentBuild.currentResult}: Job   ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}",
        recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']],
        subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
      }
    }
}