env.DOCKER_REGISTRY = 'asefamarudin'
env.DOCKER_IMAGE_NAME = 'landing-apps-prod'
pipeline {
    agent { label 'master' }
      stages {
        stage("Clone Code") {
            steps {
                script {
                checkout scm
                }
            }
        }
        stage('Building Image') {
            steps{
                script {
                    sh "docker build . -t $DOCKER_REGISTRY/$DOCKER_IMAGE_NAME:${BUILD_NUMBER}"
                }
            }
        }
        stage('Push Image') {
            steps{
                script {
                    sh "docker push $DOCKER_REGISTRY/$DOCKER_IMAGE_NAME:${BUILD_NUMBER}"
                }
            }
        }
        stage('deploy stg') {
            when{
                branch 'prod'
            }
            steps{
                script {
                    sh "kubectl  set image deployment/lp-deployment  app3=$DOCKER_REGISTRY/$DOCKER_IMAGE_NAME:${BUILD_NUMBER} -n production"
                }
            }
        }
        stage('remove docker image in local') {
            when{
                branch 'prod'
            }
            steps{
                script {
                    sh "docker rmi $DOCKER_REGISTRY/$DOCKER_IMAGE_NAME:${BUILD_NUMBER}"
                }
            }
        }
        stage('clean workspace') {

            steps{
                cleanWs()
            }
        }
        
     }
   
}
