pipeline {
    agent any
    tools { 
        maven 'Maven' 
    }

    environment {
        REPO_URL = 'https://github.com/Mani-Selvaraj/webapp.git'
        MAVEN_GOALS = 'package'
        WAR_FILE_NAME = 'your-artifact-id.war'  // Specify the actual name of your WAR file
    }

    stages {
        stage('Initialize') {
            steps {
                sh 'echo "PATH = ${PATH}" && echo "M2_HOME = ${M2_HOME}"'
            }
        }

        stage('ContinuousDownload_Build') {
            steps {
                git url: env.REPO_URL
                sh "mvn ${env.MAVEN_GOALS}"
            }
        }

        stage('ContinuousBuild_Build') {
            steps {
                git url: env.REPO_URL
                sh "mvn ${env.MAVEN_GOALS}"
            }
        }

       stage('Archive WAR File') {
    steps {
        script {
            def warFile = 'target/your-artifact-id.war'

            // Check if the WAR file exists before archiving
            if (fileExists(warFile)) {
                archiveArtifacts artifacts: warFile, onlyIfSuccessful: true, fingerprint: true
            } else {
                echo "No WAR file found at ${warFile}. Skipping archiving."
            }
        }
    }
}

    }
}
