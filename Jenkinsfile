pipeline{
    agent { label 'win' }
    
    environment {
        dotnet ='C:\\Program Files (x86)\\dotnet\\'
        }
    stages{
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
          bat "dotnet publish Calculator\\Calculator.csproj --configuration Release"
        }
      }
      stage('Sign'){
        steps{
          powershell "Submit-SigningRequest -InputArtifactPath 'Calculator\\bin\\Release\\netcoreapp3.1\\publish\\Calculator.exe' -CIUserToken 'AExbvbkphw9z/77600F+8lkotQVU4uoV6vrQ68CwXp2L' -OrganizationId '365feccb-d076-4498-80c8-4dec671b999e' -ProjectSlug 'Jenkins' -SigningPolicySlug 'TestSigning' -ApiUrl 'https://localhost:44328/'"
        }
      }
      stage('Package Artifacts'){
        steps{
          archiveArtifacts artifacts: 'Calculator\\bin\\Release\\netcoreapp3.1\\publish\\**', fingerprint: true
        }
      }
    }
}