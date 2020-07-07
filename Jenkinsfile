pipeline {
    agent any 
    stages {
        stage('Verify Branch') {
            steps {
                echo 'Hello world!'
            }
        }
        post
        {
            always{
                emailext body: 'A Test EMail', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: 'Test'
            }
        }
    }
}
