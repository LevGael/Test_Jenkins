// see https://dzone.com/refcardz/continuous-delivery-with-jenkins-workflow for tutorial
// see https://documentation.cloudbees.com/docs/cookbook/_pipeline_dsl_keywords.html for dsl reference
// This Jenkinsfile should simulate a minimal Jenkins pipeline and can serve as a starting point.
// NOTE: sleep commands are solelely inserted for the purpose of simulating long running tasks when you run the pipeline
node {
   stage 'deploy Canary'
   sh 'echo "Application fait sur Jenkinsfile"; sleep 5;'

   stage 'deploy Production'
   input 'Proceed?'
   sh 'echo "Application fait sur Jenkinsfile"; sleep 6;'
}
pipeline {
    agent any
    triggers {
        githubPush()
    }
    stages {
        stage('Restore packages'){
           steps{
               sh 'dotnet restore Test_Jenkins.sln'
            }
         }
        stage('Clean'){
           steps{
               sh 'dotnet clean Test_Jenkins.sln --configuration Release'
            }
         }
        stage('Build'){
           steps{
               sh 'dotnet build Test_Jenkins.sln --configuration Release --no-restore'
            }
         }
        stage('Test: Unit Test'){
           steps {
                sh 'dotnet test Test_Jenkins/Test_Jenkins.csproj --configuration Release --no-restore'
             }
          }
        stage('Publish'){
             steps{
               sh 'dotnet publish Test_Jenkins/Test_Jenkins.csproj --configuration Release --no-restore'
             }
        }
        stage('Deploy'){
             steps{
               sh '''for pid in $(lsof -t -i:9090); do
                       kill -9 $pid
               done'''
               sh 'cd WebApplication/bin/Release/netcoreapp3.1/publish/'
               sh 'nohup dotnet WebApplication.dll --urls="http://104.128.91.189:9090" --ip="104.128.91.189" --port=9090 --no-restore > /dev/null 2>&1 &'
             }
        }
    }
}
