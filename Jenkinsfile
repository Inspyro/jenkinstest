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
          git url: 'https://github.com/YourAcc/YourRepoName.git/', branch: 'master'
        }
      }
      stage('Restore packages'){
        steps{
          bat "dotnet restore YourProjectPath\\Your_Project.csproj"
        }
      }
      stage('Clean'){
        steps{
          bat "dotnet clean YourProjectPath\\Your_Project.csproj"
        }
      }
      stage('Build'){
        steps{
          bat "dotnet build YourProjectPath\\Your_Project.csproj --configuration Release"
        }
      }
      stage('Publish'){
        steps{
          bat "dotnet publish YourProjectPath\\Your_Project.csproj "
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