pipeline {
    agent any

    environment {
        VERSION = readMavenPom().getVersion()
        DOCKER_REPO = readMavenPom().getProperties().getProperty('docker.repository')
        IMAGE_NAME = readMavenPom().getArtifactId()

    }

    stages {

        stage('Sonar Quality Status') {
            agent {
                docker {
                    image 'maven'
               }
            }
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'sonar-token') {
                        sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }
    }


}


