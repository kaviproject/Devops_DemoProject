pipeline {
    agent any
     
    stages {
        stage('Ok') {
            steps {
                echo "Ok"
            }
        }
	    
	  stage('Restorng Packages') {
            steps {
                 bat '"C:\\Program Files (X86)\\NuGet\\nuget.exe" restore Devops_Demo.sln'
		 //bat '"C:\\Program Files (X86)\\NuGet\\nuget.exe" restore "C:\\Program Files (X86)\\Jenkins\\wokspace\\Pipeline POC1\\Devops_Demo.sln"'
            }
        }
	  stage('Build') {
            steps {
               bat "\"${tool 'MSBuild'}\\msbuild.exe\" Devops_Demo.sln /t:clean;build;package /p:PackageFileName=Devops_Demo.zip /p:ProductVersion=1.0.0.${env.BUILD_NUMBER}"
            }
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
        always {
            emailext body: 'Pipeline code testing with email service', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: 'PipelineScript Email Testing'
        }
    }
}
