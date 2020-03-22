pipeline {
  agent any
  stages {
    stage('Create infrastructure') {
      steps {
        withCredentials(bindings: [[ $class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'Aws-Capstone', accessKeyVariable: 'AWS_ACCESS_KEY_ID', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
          sh "echo this is ${env.AWS_ACCESS_KEY_ID}"
          sh "echo this is ${env.AWS_SECRET_ACCESS_KEY}"
          sh 'ansible-playbook ./ansible/ec2-launcher.yml'
          sh 'ls -la ansible'
          sh 'cat ansible/inventory'
        }
        
        sh 'ls -la /home/ubuntu/'
        sh 'cat ansible/inventory'
        sh 'ansible-playbook -i ./ansible/inventory -v ./ansible/ec2-configure.yml'
        sh 'ansible-playbook -i ./ansible/inventory -v ./ansible/k8s-deploy.yml'
        
      }
    }

  }
}