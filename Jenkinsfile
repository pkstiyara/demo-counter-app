pipeline {
    agent any

    stages {
        stage ('Git Checkout') {
            steps{
                git branch: 'main', url: 'https://github.com/pkstiyara/demo-counter-app.git'
            }
        }
        stage ('Integration Testing') {
            steps {
                sh 'mvn verify -DskipUnitTests'
            }
        }
    }
}