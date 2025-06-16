pipeline{
  agent any 

  stages{
    stage("Build stage"){
      steps{
        sh 'docker build -t node-js-sample .'
      }
    }
    stage("Test"){
      steps{
        sh 'docker run --rm node-js-sample npm test || true'
      }
    }
    stage("deploy"){
      steps{
        sh 'docker rm -f node-js-sample || true'
        sh 'docker run -d -p 5000:5000 --name node-js-sample node-js-sample'
      }
    }
  }
}
