pipeline {
  agent any
  stages{
    stage('Build'){
      steps{
        maven: "localMaven"
        sh 'mvn clean package'
      }
      post{
        success{
          echo "Now Archiving..."
          archiveArtifacts artifacts: '**/target/*.war'
        }
      }
    }
  }
}
