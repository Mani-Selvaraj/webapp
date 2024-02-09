pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                script {
                    checkout([$class: 'GitSCM', branches: [[name: '*/master']], userRemoteConfigs: [[url: 'https://github.com/Mani-Selvaraj/webapp.git']]])
                }
            }
        }

        stage('Tool Install') {
            steps {
                script {
                    tool 'Maven'
                }
            }
        }

        stage('Initialize') {
            steps {
                script {
                    withEnv(["PATH+MAVEN=${tool 'Maven'}/bin"]) {
                        echo "PATH = ${env.PATH}"
                        echo "M2_HOME = ${tool 'Maven'}"
                    }
                }
            }
        }

        stage('Continuous Download and Build') {
            steps {
                script {
                    withEnv(["PATH+MAVEN=${tool 'Maven'}/bin"]) {
                        def mvnHome = tool 'Maven'
                        def mvnCMD = "${mvnHome}/bin/mvn"
                        sh "${mvnCMD} package"
                    }
                }
            }
        }

        stage('Continuous Build') {
            steps {
                script {
                    withEnv(["PATH+MAVEN=${tool 'Maven'}/bin"]) {
                        def mvnHome = tool 'Maven'
                        def mvnCMD = "${mvnHome}/bin/mvn"
                        sh "${mvnCMD} package"
                    }
                }
            }
        }

        stage('Archive WAR File') {
            steps {
                script {
                    def warFile = "${env.WORKSPACE}/target/your-artifact-id-1.0.0-SNAPSHOT.jar"
                    if (fileExists(warFile)) {
                        archiveArtifacts artifacts: warFile, onlyIfSuccessful: true, fingerprint: true
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
