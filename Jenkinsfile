pipeline {
    agent any

    stages {
        stage ('Git Checkout') {
            steps{
                git branch: 'main', url: 'https://github.com/pkstiyara/demo-counter-app.git'
            }
        }
        stage {
            steps{
                sh 'mvn test'
            }
        }
    }
}