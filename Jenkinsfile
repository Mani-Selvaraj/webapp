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

        stage('ContinuousDownload_Build') {
            steps {
                script {
                    continuousDownloadAndBuild(env.REPO_URL, env.MAVEN_GOALS)
                }
            }
        }

        stage('ContinuousBuild_Build') {
            steps {
                script {
                    continuousDownloadAndBuild(env.REPO_URL, env.MAVEN_GOALS)
                }
            }
        }
    }
    
    def continuousDownloadAndBuild(String repoUrl, String mavenGoals) {
        git url: repoUrl
        sh "mvn ${mavenGoals}"
    }
}
