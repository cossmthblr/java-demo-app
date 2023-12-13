pipeline {
    agent any
    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "mvn1"
    }
   stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/t2mazumdar/java-demo-app.git'

                // Run Maven on a Unix agent.
                sh "mvn clean package"
            }

            post {
                success {
                    archiveArtifacts 'target/*.war'
                }
            }
        }
        stage('DockerBuild'){
            steps{
                sh "docker buildx build -t webapp -f docker ."
            }
        }
        stage('DockerContainer'){
            steps{
                 sh "docker run -d -p 30013:8080 webapp"
            }
        }
    }
}
}
post {
        success {
            mail bcc: '', body: 'Pipeline build successfully', cc: '', from: 't2mazumdar@gmail.com', replyTo: '', subject: 'The Pipeline success', to: 'cossmthblr@gmail.com'
        }
        failure {  
            mail bcc: '', body: 'Pipeline build not success', cc: '', from: 't2mazumdar@gmail.com', replyTo: '', subject: 'The Pipeline failed', to: 'cossmthblr@gmail.com'
         } 
    }
}
