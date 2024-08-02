pipeline {
    agent any

    stages {
        stage('Checkout code') {
            steps {
                // Checkout code from GitHub and specify the branch
                echo '********************************************************************************'
                echo '**************  Checkout code from GitHub and specify the branch  **************'
                git branch: 'main', url: 'https://github.com/HSGeorgiev/JenkinsSeleniumWebDriver_08_01'
            }
        }

        stage('Set up .NET Core') {
            steps {
                bat '''
                echo Installing .NET SDK 6.0
                choco install dotnet-sdk -y --version=6.0.100
                '''
            }
        }

        stage('Restore dependencies') {
            steps {
                // Restore dependencies using the solution file
                cho '********************************************************************************'
                echo '**************   Restore dependencies using the solution file   **************'
                bat 'dotnet restore SeleniumBasicExercise.sln'
            }
        }

        stage('Build') {
            steps {
                // Build the project using the solution file
                cho '********************************************************************************'
                echo '**************   Build the project using the solution file   **************'
                bat 'dotnet build SeleniumBasicExercise.sln --configuration Release'
            }
        }

        stage('Run tests TestProjects1') {
            steps {
                // Run tests using the solution file
                cho '********************************************************************************'
                echo '**************   Run tests using the solution file   **************'
                bat 'dotnet test TestProject1/TestProject1.csproj --logger "trx;LogFileName=TestResults.trx"'
            }
        }

                stage('Run tests TestProjects2') {
            steps {
                // Run tests using the solution file
                cho '********************************************************************************'
                echo '**************   Run tests using the solution file   **************'
                bat 'dotnet test TestProject2/TestProject2.csproj --logger "trx;LogFileName=TestResults.trx"'
            }
        }

                stage('Run tests TestProjects3') {
            steps {
                // Run tests using the solution file
                cho '********************************************************************************'
                echo '**************   Run tests using the solution file   **************'
                bat 'dotnet test TestProject3/TestProject3.csproj --logger "trx;LogFileName=TestResults.trx"'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/TestResults/*.trx', allowEmptyArchive: true
            step([
                $class: 'MSTestPublisher',
                testResultsFile: '**/TestResults/*.trx'
            ])

        }
    }


}
