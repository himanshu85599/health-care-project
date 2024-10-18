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
    }
}
