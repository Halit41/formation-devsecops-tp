pipeline {
  agent any

  stages {
      stage('Build Artifact') {
      steps {
        sh 'mvn clean package -DskipTests=true'
        archive 'target/*.jar' //so that they can be downloaded later test aa
      }
      }

    //--------------------------
    stage('Docker Build and Push') {
      steps {
        withCredentials([string(credentialsId: 'DOCKER_HUB_PASSWORD_HALIT', variable: 'password')]) {
          sh 'sudo docker login -u halit4141 -p $password'
          sh 'printenv'
          sh 'sudo docker build -t halit4141/devops-app:latest .'
          sh 'sudo docker push halit4141/devops-app:latest'
        }
      }
    }

    // //--------------------------
    // stage('Deployment Kubernetes  ') {
    //   steps {
    //     withKubeConfig([credentialsId: 'configtssraks']) {
    //       sh "sed -i 's#replace#halit4141/devops-app:${GIT_COMMIT}#g' k8s_deployment_service.yaml"
    //       sh 'kubectl apply -f k8s_deployment_service.yaml'
    //     }
    //   }
    // }
  }
}
