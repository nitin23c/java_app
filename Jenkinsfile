@Library('my-jenkins-library') _
pipeline {
    agent any

    stages{
        stage('Git Checkout'){
            steps{
                script{
                    gitCheckout(
                    branch: "main",
                    credentialsId: "github",
                    url:"git@github.com:nitin23c/java_app.git")
            }
            }
        }
    }
}