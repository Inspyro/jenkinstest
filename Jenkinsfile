pipeline{
    agent { label 'win' }
    
    environment {
        dotnet ='C:\\Program Files (x86)\\dotnet\\'
        }
    stages{
      stage('Restore packages'){
        steps{
          bat "dotnet restore Calculator\\Calculator.csproj"
          bat "hostname"
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
      stage('Package Artifacts'){
        steps{
          archiveArtifacts artifacts: 'Calculator\\bin\\Release\\netcoreapp3.1\\publish\\**', fingerprint: true
        }
      }
      stage('SignPath'){
          steps{
              submitSigningRequest(apiUrl: "http://localhost:44328/", 
                                   ciUserToken: "AH/I3MoDI8pBUd5rJbWst9VsPoh05OQ5pxQE2ZHEzQoY", 
                                   organizationId: "5278a79c-5e5d-440d-994a-1d7901849ea7",
                                   projectSlug: "SomeProject",
                                   signingPolicySlug: "TestSigning",
                                   inputArtifactPath: "Calculator\\bin\\Release\\netcoreapp3.1\\publish\\Calculator.exe",
                                   outputArtifactPath: "Calculator.signed.exe",
                                   waitForCompletion: true,
                                   serviceUnavailableTimeoutInSeconds: 20,
                                   uploadAndDownloadRequestTimeoutInSeconds: 20,
                                   waitForCompletionTimeoutInSeconds: 20)
          }
      }
    }
}
