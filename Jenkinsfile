def NUGETPKG_LOCATION="C:\\Program Files (X86)\\NuGet\\nuget.exe"
def SOLUTION_NAME="Devops_Demo"
pipeline {
    agent any
	  parameters {
        //string(defaultValue: "", description: 'K', name: 'HELLO')
        choice(choices: ['Windows', 'Linux'], description: 'What OS?', name: 'PickAnOS')
    }
     environment {
        CONFIG = 'Release'
	NUGETPKG_LOCATION="C:\\Program Files (X86)\\NuGet\\nuget.exe"
	SOLUTION_NAME="Devops_Demo"
          }
	
    stages {
	     stage('PrintParameter'){
            steps{
               // echo "${params.HELLO}"
		     echo "${params.PickAnOS}"
		    
            }
        }
        stage('environment variable checking') {
		
		
		when {
			 branch 'refs/remotes/origin/master'
		    }
            steps {
                echo "$GIT_BRANCH"
		//echo "${env.CONFIG}"
		//echo "${env.NUGETPKG_LOCATION}"
		//powershell 'Write-Output "Hello, World!"'
		    
            }
        }  
	     stage('Sanity check') {
            steps {
                input "Does the staging environment look ok?"
            }
     }
	  stage('Restoring Packages') {
            steps {
		   // bat '"C:\\Program Files (X86)\\NuGet\\nuget.exe" restore ${SOLUTION_NAME}.sln'
                 bat '"C:\\Program Files (X86)\\NuGet\\nuget.exe" restore Devops_Demo.sln'
		 //bat '"C:\\Program Files (X86)\\NuGet\\nuget.exe" restore "C:\\Program Files (X86)\\Jenkins\\wokspace\\Pipeline POC1\\Devops_Demo.sln"'
            }
        }
	  stage('Build') {
            steps {
               bat "\"${tool 'MSBuild'}\\msbuild.exe\" Devops_Demo.sln /t:clean;build;package /p:PackageFileName=Devops_Demo.zip /p:ProductVersion=1.0.0.${env.BUILD_NUMBER}"
            }
        }
	 stage('Approve PROD Deploy') {
         when {
            branch 'origin/master'
         }
         options {
            timeout(time: 1, unit: 'HOURS') 
         }
         steps {
            input message: "Deploy?"
         }
         post {
            success {
               echo "Production Deploy Approved"
            }
            aborted {
               echo "Production Deploy Denied"
            }
         }
      }
	     stage('Deploy')
    {
        withCredentials([usernamePassword(credentialsId: '4b9640e9-311b-4539-8b0d-064ba3df7ea7', passwordVariable: 'STAGING_PASSWORD', usernameVariable: 'STAGING_USERNAME')]) {
             echo "$STAGING_USERNAME"
    // some block
  
      // bat 'C:\\"Program Files (x86)"\\IIS\\"Microsoft Web Deploy V3"\\msdeploy.exe -verb:sync -source:package="C:\\Program Files (x86)\\Jenkins\\workspace\\POCPIPELINE\\TestJenkin_VS2019\\obj\\Release\\Package\\TestJenkin_VS2019.zip" -dest:auto,computername=%TRAGET_SERVER%,username=%STAGING_USERNAME%,password=%STAGING_PASSWORD% -setParam:name="IIS Web Application Name",value="Default Web Site\\ParupatikComputerCDDeploy"'
    }
        //stage 'Checkout'
		//checkout scm

	//stage 'Build'
		//bat 'nuget restore SolutionName.sln'
		//bat "\"${tool 'MSBuild'}\" SolutionName.sln /p:Configuration=Release /p:Platform=\"Any CPU\" /p:ProductVersion=1.0.0.${env.BUILD_NUMBER}"

	//stage 'Archive'
		//archive 'ProjectName/bin/Release/**'
    }
    post {
        failure {
            emailext body: 'Pipeline code testing with email service', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: 'PipelineScript Email Testing'
        }
    }
}
