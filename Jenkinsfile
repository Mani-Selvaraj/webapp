pipeline {
    agent any
    tools { maven 'Maven' }
    
    environment {
        REPO_URL = 'https://github.com/Mani-Selvaraj/webapp.git'
        MAVEN_GOALS = 'package'
    }

    stages {
        stage('Initialize') {
            steps {
                sh 'echo "PATH = ${PATH}" && echo "M2_HOME = ${M2_HOME}"'
            }
        }

        def continuousDownloadAndBuild(String repoUrl, String mavenGoals) {
            steps {
                git url: repoUrl
                sh "mvn ${mavenGoals}"
            }
        }

        stage('ContinuousDownload_Build') {
            steps {
                continuousDownloadAndBuild(env.REPO_URL, env.MAVEN_GOALS)
            }
        }

        stage('ContinuousBuild_Build') {
            steps {
                continuousDownloadAndBuild(env.REPO_URL, env.MAVEN_GOALS)
            }
        }
    }
}
