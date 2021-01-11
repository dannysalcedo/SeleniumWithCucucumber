pipeline {
  agent any
  stages {
    stage('Build and Test') {
      parallel {

      stage('checkuot') {
          steps {
            echo 'Cheking from GitHub'
             git 'https://github.com/dannysalcedo/SeleniumWithCucucumber.git'
          }     
      }
      stage('Build and Test') {
          steps {
            echo 'Clean Previous Build Project'
            sh(script: 'mvn clean', label: 'maven Clean')
          }
          steps {
            echo 'Compiling Project'
            sh(script: 'mvn compile', label: 'maven Compile')
          }
          steps {
            echo 'Testing Project'
            sh(script: 'mvn verify', label: 'maven Test')
          }
      }
      stage('Cucumber') {
          steps {
            cucumber failedFeaturesNumber: -1, failedScenariosNumber: -1, failedStepsNumber: -1, fileIncludePattern: '**/*.json', pendingStepsNumber: -1, skippedStepsNumber: -1, sortingMethod: 'ALPHABETICAL', undefinedStepsNumber: -1
          }
      }
      stage('Email Notification') {
        steps {
          emailext body: '''Build Execution Complete With 
                          Ckeckout+ Compile + Package + Reporting''', subject: 'Build and Execution Completed', to: 'DevOps@Automation.com'
        }
      }
    }
  }
}


