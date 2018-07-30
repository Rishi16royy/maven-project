pipeline {
  agent any
  stages{
    stage('Build'){
      steps{
        maven: "/usr/local/Cellar/maven/3.5.3/libexec"
        sh 'mvn clean package'
      }
      post{
        success{
          echo "Now Archiving..."
          archiveArtifacts artifacts: '**/target/*.war'
        }
      }
    }
    stage('Deploy to Staging'){
      steps {
        build job: "deploy-to-staging"
      }
    }
  }
}
