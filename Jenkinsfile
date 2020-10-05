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
              submitSigningRequest(apiUrl: "https://localhost:44328", 
                                   ciUserToken: "ALJDSw8TXY8Qg+DMPwEIDNvu3ZgvmE4btg2tWXNjc19h", 
                                   organizationId: "c3bb3384-ae65-4bc5-93ad-2537e4fc87b6",
                                   projectSlug: "Teamcity",
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
