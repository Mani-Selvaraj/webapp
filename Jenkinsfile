pipeline {
    agent any
    tools { 
        maven 'Maven' 
    }
    stages {
        stage('Initialize') {
            steps {
                sh 'echo "PATH = ${PATH}" && echo "M2_HOME = ${M2_HOME}"'
            }
        }

        def continuousDownloadAndBuild = {
            steps {
                git 'https://github.com/Mani-Selvaraj/webapp.git'
                sh 'mvn package'
            }
        }

        stage('ContinuousDownload_Build') {
            steps(continuousDownloadAndBuild)
        }

        stage('ContinuousBuild_Build') {
            steps(continuousDownloadAndBuild)
        }
    }

    post {
        success {
            archiveArtifacts 'target/*.war'
        }
    }
}
