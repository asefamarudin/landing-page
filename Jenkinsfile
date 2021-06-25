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
                    sh "docker build . -t asefamarudin/landing-apps:${BUILD_NUMBER}"
                }
            }
        }
        stage('Push Image') {
            steps{
                script {
                    sh "docker push asefamarudin/landing-apps:${BUILD_NUMBER}"
                }
            }
        }
        stage('deploy') {
            steps{
                script {
                    sh "kubectl  set image deployment/sosmed-cilsy  sosmed-cilsy=asefamarudin/landing-apps:${BUILD_NUMBER}"
                }
            }
        }
     }
   
}
