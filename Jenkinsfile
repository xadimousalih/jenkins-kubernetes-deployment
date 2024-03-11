pipeline {
  environment {
    dockerimagename = 'xadimousalih/react-app'
  //dockerImage = ""
  }
  agent any
  stages {
    stage('Checkout Source') {
      steps {
            git url: 'https://github.com/xadimousalih/jenkins-kubernetes-deployment.git', branch: 'main', credentialsId: 'GitHub_Credentials'
      }
    }
    stage('Build image') {
      steps {
        script {
          dockerImage = docker.build dockerimagename
        }
      }
    }
    stage('Pushing Image') {
      environment {
          registryCredential = 'Docker_Hub_Credentials'
      }
      steps {
        script {
          docker.withRegistry('https://registry.hub.docker.com', registryCredential) {
            dockerImage.push('latest')
          }
        }
      }
    }
    // stage('Deploying React.js container to Kubernetes') {
    //   steps {
    //     //container(name: 'kubectl', shell: '/bin/sh') {
    //       withKubeConfig([credentialsId: 'kubernetes-config'])
    //                    //[credentialsId: '<credential-id>', caCertificate: '<ca-certificate>', serverUrl: '<api-server-address>', contextName: '<context-name>', clusterName: '<cluster-name>', namespace: '<namespace>']
    //       {
    //         //sh 'curl -LO "https://storage.googleapis.com/kubernetes-release/release/v1.20.5/bin/linux/amd64/kubectl"'
    //         //sh 'chmod u+x ./kubectl'
    //         //sh "echo SANTE BOROM TOUBA"
    //         //sh './kubectl get pods'
    //         //sh 'minikube kubectl -- get pods'
    //         //sh 'kubectl get pods'

    //         sh "kubectl apply -f deployment.yaml"
    //         sh "kubectl apply -f service.yaml"
    //       }
    //     //}
    //   }
    // }

    stage('Deploy') { 
      steps { 
        container('kubectl') { 
          sh 'kubectl apply -f deployment.yaml'
          sh 'kubectl apply -f service.yaml' 
        } 
      } 
    }
  }
}
