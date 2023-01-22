pipeline {
    agent any

    stages {
        stage ('Git Checkout') {
            steps{
                git branch: 'main', url: 'https://github.com/pkstiyara/demo-counter-app.git'
            }
        }
        stage ('UNIT Testing') {
            steps{
                sh 'mvn test'
            }
        }
        stage ('Integration Testing') {
            steps {
                sh 'mvn verify -DskipUnitTests'
            }
        }
        stage ('Maven Build'){
            steps{
                sh 'mvn clean install'
            }
        }
        stage ('Static Code analysis'){
            steps{

            }
        }
        stage('Docker Image Build'){
            steps{
                script {
                    sh 'docker image build -t $JOB_NAME:v1.$BUILD_ID'
                    sh 'docker image tag $JOB_NAME:v1.$BUILD_ID pkstiyara/$JOB_NAME:latest'
                }
            }
        }
        stage ('push image to the dockerHub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'git_creds', variable: 'docker_hub_cred')]) 
                    {
                        sh 'docker login -u pkstiyara -p $(docker_hub_cred)'
                        sh 'docker image push pkstiyara/$JOB_NAME:v1.$BUILD_ID'
                        sh 'docker image push pkstiyara/$JOB_NAME:latest'
                    }
                }
            }
        }
    }
}