pipeline {
    agent any 
    stages {
        stage('Verify Branch') {
            steps {
                echo 'Hello world!' 
                checkout scm
                 sh "echo Hello from the shell"
                sh "hostname"
                sh "uptime"
            }
        }
    }
}
