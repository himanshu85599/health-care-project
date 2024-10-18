pipeline {
    agent any
    tools {
        maven 'M2_HOME'
    }
    
    stages {
        stage('Git Checkout') {
            steps {
                echo 'This stage is to clone the repo from GitHub'
                git branch: 'master', url: 'https://github.com/himanshu85599/health-care-project'
            }
        }
        stage('Create Package') {
            steps {
                echo 'This stage will compile, test, and package my application'
                sh 'mvn package'
            }
        }
        stage('Generate Test Report') {
            steps {
                echo 'This stage generates the Test report using TestNG'
                publishHTML([
                    allowMissing: false, 
                    alwaysLinkToLastBuild: false, 
                    keepAll: false, 
                    reportDir: 'target/surefire-reports', 
                    reportFiles: 'index.html', 
                    reportName: 'HTML Report', 
                    reportTitles: '', 
                    useWrapperFileDirectly: true
                ])
            }
        }
        stage('Create Docker Image') {
      steps {
        echo 'This stage will Create a Docker image'
        sh 'docker build -t himax85599/healthcare:1.0 .'
                          }
            }
     stage('Login to Dockerhub') {
      steps {
        echo 'This stage will loginto Dockerhub' 
        withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'dockerpass', usernameVariable: 'dockeruser')]) {
        sh 'docker login -u ${dockeruser} -p ${dockerpass}'
         }
      }
     }
    stage('Docker Push-Image') {
      steps {
        echo 'This stage will push my new image to the dockerhub'
        sh 'docker push himax85599/healthcare:1.0'
            }
      }
    }
}
