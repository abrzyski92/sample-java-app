pipeline {
    agent { agent1 }

   tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven3.9.8"
    }


    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                
                git branch: 'main', credentialsId: 'github_ssh_abrzyski92', url: 'https://github.com/abrzyski92/sample-java-app.git'
                

                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
                
                sh 'echo "SUCCESS"'

            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    mail bcc: '', body: 'sample_body', cc: '', from: '', replyTo: '', subject: 'Jenkis Pipeline Notification', to: 'abrzyski92@gmail.com'
                }
            }
        }
    }
}
