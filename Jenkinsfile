pipeline {
  agent any
  tools{
    maven 'localMaven'
  }
  stages{
    stage('Build'){
      steps{
        sh 'mvn clean package'
      }
      post{
        success{
          echo "Now Archiving..."
          archiveArtifacts '**/*.war'
        }
      }
    }
    stage('Deploy to Staging'){
      steps {
        build job: "deploy-to-staging-jenkinsfile"
      }
    }
    stage('Deploy to Production'){
      steps{
        timeout(time:5, unit:'DAYS'){
          input message: 'Approve Production Deployment ?'
        }

        build job: 'deploy-to-prod-jenkinsfile'
      }
      post{
        success{
          echo "Code deployed to Prod."
        }
        failure{
          echo "Deployment failed"
        }
      }
    }
  }
}
