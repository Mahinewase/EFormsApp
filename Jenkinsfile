pipeline {
    agent any 
    
    triggers {
        cron('H/15 * * * *')
    }
    
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Mahinewase/EFormsApp.git'
            }
        }
        
        stage('Build') {
            steps {
                bat 'msbuild WebApplication.sln'
            }
        }
        
        stage('Test') {
            steps {
                bat 'dotnet test WebApplication.Tests.csproj'
            }
        }
        
        stage('Code Review') {
            steps {
                bat 'dotnet sonarscanner begin /k:"aspnet-app" /d:sonar.host.url="http://sonarqube:9000" /d:sonar.login="admin" /d:sonar.password="admin"'
                bat 'msbuild /t:Rebuild' 
                bat 'dotnet sonarscanner end'
            }
        }
    } 
}
