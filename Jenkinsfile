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
              submitSigningRequest(organizationId: "C6844362-9816-440A-9C41-A28513C8FE64")
          }
      }
      stage('Sign'){
        input {
            id "WaitForSign"
            message "Should we sign the project?"
        }
        steps{
            echo "Build Url: " + env.BUILD_URL
            echo "Build Number: " + env.BUILD_NUMBER
            echo "Job Name: " + env.JOB_NAME
            echo "something"
            powershell "Submit-SigningRequest -InputArtifactPath 'Calculator\\bin\\Release\\netcoreapp3.1\\publish\\Calculator.exe' -CIUserToken 'AExbvbkphw9z/77600F+8lkotQVU4uoV6vrQ68CwXp2L' -OrganizationId '365feccb-d076-4498-80c8-4dec671b999e' -ProjectKey 'Jenkins' -SigningPolicyKey 'TestSigning' -ApiUrl 'https://localhost:44328/'"
        }
      }
    }
}
