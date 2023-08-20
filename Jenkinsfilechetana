node{
 echo "Jenkins home dir is : ${env.JENKINS_HOME}"
 echo "Job name is : ${env.JOB_NAME}"
 echo "Build number is : ${env.BUILD_NUMBER}"   
 
 properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '', numToKeepStr: '6')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])
    
def mavenHome = tool name: 'maven3.9.3'
    
stage('CheckOutCode'){
git branch: 'development', credentialsId: '9a631ac0-0599-4e84-8bae-016a6e2fb52b', 
url: 'https://github.com/ChetanaSri/maven-web-application.git'
}
stage('Build'){
sh "${mavenHome}/bin/mvn clean package"
}
stage('ExecuteSonarQubeReport'){
sh "${mavenHome}/bin/mvn clean sonar:sonar"
}
/*
stage('UploadArtifactsInotNexus'){
sh "${mavenHome}/bin/mvn clean deploy"
}

stage('DeploAppIntoTomcatServer'){
sshagent(['9a8e571c-60ab-4c0a-af3a-02bb16942249']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@172.31.39.91:/opt/apache-tomcat-9.0.76/webapps/"
}
}
*/
}
