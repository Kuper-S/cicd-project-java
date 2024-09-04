pipeline{
    agent{
        label 'jenkins-jenkins-agent'
        defaultContainer 'jnlp'
    }
    tools {
        jdk 'Java17'
        maven 'Maven3'
    }
    environment {
        APP_NAME = "e2e-pipeline-app"
        RELEASE = "1.0.0"
        DOCKER_USER = credentials('dockerhub-credentials').username
        DOCKER_PASS = credentials('dockerhub-credentials').password
        IMAGE_NAME = "${DOCKER_USER}" + "/" + "${APP_NAME}"
        IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
        JENKINS_API_TOKEN = credentials("JENKINS_API_TOKEN")

    }
    stages{
        stage("Cleanup Workspace"){
            steps {
                cleanWs()
            }

        }
    
        stage("Checkout from SCM"){
            steps {
                checkout([
                    $class: 'GitSCM', 
                    branches: [[name: '*/main']], 
                    userRemoteConfigs: [[url: 'https://github.com/Kuper-S/cicd-project-java.git', credentialsId: 'github-credentials']]
                ])
            }

        }

        stage("Build Application"){
            steps {
                sh "mvn clean package"
                echo("BLBLBA")
            }

        }

        stage("Test Application"){
            steps {
                sh "mvn test"
            }
        }
    }
}
