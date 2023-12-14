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
                 sh "docker run -d --name my-demo-con -p 30013:8080 webapp"
            }
        }
    }
}
