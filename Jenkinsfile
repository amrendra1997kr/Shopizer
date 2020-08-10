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
    stage ('Build Docker Image') {
      steps{
        echo "Building Docker Image"
        sh '''
            cd sm-shop
            docker build "Dockerfile" -t 7903539838/shopizer:latest
          '''
      }
    }
    stage ('Push Docker Image') {
      steps{
        echo "Pushing Docker Image"
      }
    }
    stage ('Deploy to Dev') {
      steps{
        echo "Deploying to Dev Environment"
      }
    }
  }
}
