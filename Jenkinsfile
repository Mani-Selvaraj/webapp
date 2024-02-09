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

 node('master') 
{
    stage('ContinuousDownload_Master') 
    {
         git 'https://github.com/Mani-Selvaraj/webapp.git'
        
    }
     stage('ContinuousBuild_Master') 
    {
        sh 'mvn package'
    }    
 }
        }
      }

   }
}  
