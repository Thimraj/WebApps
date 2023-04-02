#!groovy

properties([
    buildDiscarder(logRotator(numToKeepStr: '1')),
    pipelineTriggers([
        pollSCM('* * * * *')
    ])
])


node{
    
    stage('CheckOutCode'){
        git branch: 'main', credentialsId: 'javahome2', url: 'https://github.com/Thimraj/WebApps.git'
    }
    
    stage('Build'){
      if(isUnix()){
          sh 'mvn clean package'
      }else{
          bat 'mvn clean package'
      }
    }
    /*
    stage('SonarQubeReport'){
      if(isUnix()){
          sh 'mvn  sonar:sonar'
      }else{
          bat 'mvn sonar:sonar'
      }
    }
    
     stage('UploadintoNexus'){
      if(isUnix()){
          sh 'mvn  deploy'
      }else{
          bat 'mvn deploy'
      }
    }
    stage('DeployAppIntoTomcat'){
        sh 'echo App is deploying into tomcat server'
        sh 'cp $WORKSPACE/target/maven-web-application.war /Users/mithunreddy/MithunTechnologies/Softwares/Running/apache-tomcat-9.0.14/webapps/'
        sh 'echo Deployed the into Tomcat successsfully' 
    }
    */
    stage('SendEmailNotification'){
        mail bcc: 'mtrdevopsr@gmail.com', body: '''Build Done.
        Regards,
        Mithun Technologies,
        9980923226.
        ''', cc: 'mtrdevops@gmail.com', from: 'thimrajdevops@gmail.com', replyTo: 'mtrdevops@gmail.com', subject: 'Duild done', to: 'mtrdevops@gmail.com'
    }
    
    stage('SendSlackNotifications'){
        
        slackSend baseUrl: 'https://devops-team-bangalore.slack.com/services/hooks/jenkins-ci/', channel: 'build-notification', color: 'black', message: 'Build sent to Slack', tokenCredentialId: '9558055f-b9e7-485a-a61c-898e24fa0678'
    }
    
    }
