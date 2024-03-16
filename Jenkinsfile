pipeline {
    agent any
    environment {
        DOCKER_REGISTRY = 'saidocker999/musicplayer'
    }
      tools {
        dockerTool 'docker'
    }


    stages {
        stage('Docker Build') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-password') {
                               def customImage = docker.build("saidocker999/reactapp:${env.BUILD_ID}")

                            /* Push the container to the custom Registry */
                            customImage.push()
                    }
                }
            }
        }
        stage('test'){
            steps{
                script{
                    def scannerHome = tool 'sonar';
                    withSonarQubeEnv(credentialsId: 'sonar-pass') {
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=reactapp" 

                    }
                }
            }
        }
    }
}

