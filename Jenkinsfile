pipeline {
    agent any 
    tools {
        maven 'Maven'
    }
    stages {
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                ''' 
            }
        }

        stage('ContinuousDownload_Build') {
            steps {
                git 'https://github.com/Mani-Selvaraj/webapp.git'
            }
        }

        stage('ContinuousBuild_Build') {
            steps {
                sh 'mvn package'
            }
        }

        stage('ContinuousDownload_Master') {
            // You can specify the node here or within the steps of this stage
            steps {
                node('master') {
                    git 'https://github.com/Mani-Selvaraj/webapp.git'
                }
            }
        }

        stage('ContinuousBuild_Master') {
            // You can specify the node here or within the steps of this stage
            steps {
                node('master') {
                    sh 'mvn package'
                }
            }
        }
    }
}
