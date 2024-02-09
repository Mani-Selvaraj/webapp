pipeline {
    agent any

    stages {
        // ... (previous stages remain unchanged)

        stage('Archive WAR File') {
            steps {
                script {
                    def warFile = "${env.WORKSPACE}/target/your-artifact-id-1.0.0-SNAPSHOT.jar"
                    if (fileExists(warFile)) {
                        archiveArtifacts artifacts: "target/your-artifact-id-1.0.0-SNAPSHOT.jar", onlyIfSuccessful: true, fingerprint: true
                    } else {
                        error "WAR file not found or build was unsuccessful"
                    }
                }
            }
        }
    }

    post {
        failure {
            echo "Build failed. Please check the logs for more information."
        }
    }
}
