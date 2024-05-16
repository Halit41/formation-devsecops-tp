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
        withCredentials([string(credentialsId: 'docker-hub-password-achraf', variable: 'DOCKER_HUB_PASSWORD_HALIT')]) {
          sh 'sudo docker login -u halit4141 -p $DOCKER_HUB_PASSWORD'
          sh 'printenv'
          sh 'sudo docker build -t halit4141/devops-app:""$GIT_COMMIT"" .'
          sh 'sudo docker push halit4141/devops-app:""$GIT_COMMIT""'
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
