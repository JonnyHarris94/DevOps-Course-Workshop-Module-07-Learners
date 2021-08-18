pipeline {
    agent none

    stages {
        stage('Build C# Code') {
            agent {
                docker {image 'mcr.microsoft.com/dotnet/sdk:5.0'}
            }
            steps {
                sh 'dotnet build'
            }
        }
        stage('Dotnet Test'){
            agent {
                docker {image 'mcr.microsoft.com/dotnet/sdk:5.0'}
            }
            steps{
                sh 'dotnet test'
            }
        }
        stage('Build TypeScript') {            
            agent {
                docker {image 'node:14-alpine'}
            }
            steps {
                dir ('./DotnetTemplate.Web'){
                    sh '''
                        npm install
                        npm run build
                    '''
                }
            }
        }
        stage('TypeScript Tests'){
            agent {
                docker {image 'node:14-alpine'}
            }
            steps{
                dir ('./DotnetTemplate.Web'){
                    sh '''
                        npm t
                        npm run lint
                    '''
                }
            }
        }
    }
}