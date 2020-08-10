pipeline{
  environment{
    registry = "7903539838/shopizer"
    registryCredential = 'Docker_Hub_Amrendra'
    dockerImage = ''
  }
  agent any
  stages{
    stage ('Build') {
      steps{
        echo "Building Project"
        sh 'mvn clean install -DskipTests=True'
      }
    }
    stage{
      steps{
        echo "Archiving Project"
        script{
          archiveArtifacts artifacts: '**/*.war', followSymlinks: false
        }
      }
    }
    stage ('Build Docker Image') {
      steps{
        echo "Building Docker Image"
        script{
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage ('Push Docker Image') {
      steps{
        echo "Pushing Docker Image"
        script{
          docker.withRegistry ('' , registryCredential  ) {
            dockerImage.push()
            dockerImage.push('latest')
          }
        }
      }
    }
    stage ('Deploy to Dev') {
      steps{
        echo "Deploying to Dev Environment"
        sh "docker rm -f shopizer || true"
        sh "docker run -d --name=shopizer -p 8082:8080 7903539838/shopizer"
      }
    }
  }
}
