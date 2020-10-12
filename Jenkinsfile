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
                                   ciUserToken: "AJb2OOqIwTZEUFv6b1me2S6wH1VV2jOpSynz3cQ5RU/r", 
                                   organizationId: "5278a79c-5e5d-440d-994a-1d7901849ea7",
                                   projectSlug: "SomeProject",
                                   signingPolicySlug: "TestSigning",
                                   inputArtifactPath: "Calculator\\bin\\Release\\netcoreapp3.1\\publish\\Calculator.exe",
                                   outputArtifactPath: "Calculator.signed.exe",
                                   waitForCompletion: true,
                                   serviceUnavailableTimeoutInSeconds: 10,
                                   uploadAndDownloadRequestTimeoutInSeconds: 10,
                                   waitForCompletionTimeoutInSeconds:10)
          }
      }
    }
}
