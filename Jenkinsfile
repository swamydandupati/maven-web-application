node{ 
    def mavenHome = tool name: "maven3.8.2"
    
    stage('CheckOutCode')
    {
        git branch: 'development', credentialsId: '8729c0e7-2b96-46eb-91e3-940ec53852d0', url: 'https://github.com/swamydandupati/maven-web-application.git'
    }
    
    stage('Build')
    {
      sh "${mavenHome}/bin/mvn clean package"  
    }

    stage('SonarQubeReport')
    {
      sh "${mavenHome}/bin/mvn clean package sonar:sonar"    
    }
    
/*
    stage('UploadArtifactintiNexus')
    {
      sh "${mavenHome}/bin/mvn clean package sonar:sonar deploy"    
    }
    
    
    stage('DeployAppIntoTomcatServer')
    {
      sshagent(['39915b97-7aa2-451c-9822-e840680cf812']) {
       sh "scp -o  StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.88.109.40:/opt/apache-tomcat-9.0.65/webapps"

}  
    }
*/    
stage('SendEmailNotification')
    { 
      emailext body: '''Build is over,
Regards,
Swamy,
6304091849''', subject: 'buildisover...!!!', to: 'dswamy023@gmail.com'
    }
    
}    
