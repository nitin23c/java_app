@Library('my-jenkins-library') _
pipeline {
    agent any

    parameters{

        choice(name: 'action', choices: 'create\ndestroy', description: 'Choose to either create or destroy')
        string(name: 'imageName', description: "name of the docker image", defaultvalue: 'java-app')
        string(name: 'ImageTag', description: "tag of the docker build", defaultvalue: 'v1')
        string(name: 'appName', description: "name of the Application", defaultvalue: 'springboot')
    }

    stages{
        stage('Git Checkout'){
            when { expression { params.action == 'create' } }
            steps{
                script{
                    gitCheckout(
                    branch: "main",
                    credentialsId: "github",
                    url:"git@github.com:nitin23c/java_app.git")
            }
            }
        }

        stage('Unit Test Maven'){
            when { expression { params.action == 'create' } }
            steps{
                script{
                     mvnTest()
                }
            }
        }

        stage('Integration Test Maven'){
            when { expression { params.action == 'create' } }
            steps{
                script{
                     mvnIntegrationTest()
                }
            }
        }

        stage('Static code analysis: sonarqube'){
            when { expression { params.action == 'create' } }
            steps{
                script{
                    def SonarQubecredentialsId = 'sonarqube-api'
                     staticCodeAnalysis(SonarQubecredentialsId)
                }
            }
        }

        stage('Quality Gate Status check : sonarqube'){
            when { expression { params.action == 'create' } }
            steps{
                script{
                    def SonarQubecredentialsId = 'sonarqube-api'
                     qualityGateStatus(SonarQubecredentialsId)
                }
            }
        }

        stage('Maven Build : maven'){
            when { expression { params.action == 'create' } }
            steps{
                script{
                    mvnBuild()
                }
            }
        }

        stage('Docker Image Build'){
            when { expression { params.action == 'create' } }
            steps{
                script{
                    dockerBuild("${params.imageName}", "${params.imageTag}", "${params.appName}")
                }
            }
        }
    }
}