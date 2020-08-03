pipeline{
    agent any
    
    environment {
        dotnet ='C:\\Program Files (x86)\\dotnet\\'
        }
    stages{
      stage('Restore packages'){
        steps{
          sh "dotnet restore Calculator\\Calculator.csproj"
        }
      }
      stage('Clean'){
        steps{
          sh "dotnet clean Calculator\\Calculator.csproj"
        }
      }
      stage('Build'){
        steps{
          sh "dotnet build Calculator\\Calculator.csproj --configuration Release"
        }
      }
      stage('Publish'){
        steps{
          sh "dotnet publish Calculator\\Calculator.csproj "
        }
      }
    }
}