pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/paekseobin-crypto/ktcloudinfrajenkins.git', branch: 'main'
      }
    }
    stage('docker image build and push to hub') {
      steps {
        sh '''
        docker build -t paekseobin/ktcloudinfra4:0727
        docker push paekseobin/ktcloudinfra4:0727
        '''
      }
    }
    
    
    stage('delivery and deployment using k8s') {
      steps {
        sh '''
        ansible master -m copy -a "src=deploy.yml dest=/root/deploy.yml"
        ansible master -m shell -a "kubectl --kubeconfig=/etc/kubernetes/admin.conf apply -f deploy.yml"
        '''
      }
    }
  }
}
