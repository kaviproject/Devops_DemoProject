pipeline {
    agent any
     
    stages {
        stage('Ok') {
            steps {
                echo "Ok"
            }
        }
	    stage()
	    {
		    bat 'nuget restore Devops_Demo.sln'
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
