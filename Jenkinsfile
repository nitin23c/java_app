pipeline {
    agent any

    stages{
        stage('Git Checkout'){
            steps{
                script{
                    git branch: 'main', credentialsId: 'github', url: 'git@github.com:nitin23c/java_app.git'
            }
            }
        }
    }
}