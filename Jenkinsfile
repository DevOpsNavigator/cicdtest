pipeline{
  agent any
  stages {
    stage('git scm update'){
      steps{
        git url: 'https://github.com/DevOpsNavigator/cicdtest.git', branch: 'main'
      }
    }
    stage('docker build and push'){
      steps{
        sh '''
        sudo docker build -t walloonam/cicdtest:gold .
        sudo docker push walloonam/cicdtest:gold
        '''
      }
    }
    stage('deploy kubernetes'){
      steps{
        sh '''
        ansible master -m command -a 'sudo kubectl create deploy piplineweb --image=walloonam/cicdtest:gold'
        ansible master -m command -a 'sudo kubectl expose deploy piplineweb --type=LoadBalancer --port=80 --target-port=80 --name=piplineweb'
        '''
      }
    }  
  }
}
