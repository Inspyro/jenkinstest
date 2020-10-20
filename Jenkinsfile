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
              submitSigningRequest(apiUrl: "https://sp-dev-web.dev.rubicon-it.com/SignPath.Application_green-rev1/Api", 
                                   ciUserToken: "AB2etCntzCMqpzsL4jhtwD466c7KBzr7opkx/810yXdq", 
                                   organizationId: "680cf22e-f36d-4bbe-8bd0-8a722be51b90",
                                   projectSlug: "CalculatorProject",
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
