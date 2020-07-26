
node
{
    
def mavenHome = tool name: "Maven3.6.3"

stage ('clone-code'){
git branch: 'development', credentialsId: 'gitCredentials', url: 'https://github.com/mylandmarktech/maven-web-application.git'
}
stage ('Build'){
sh "${mavenHome}/bin/mvn clean package"
}

stage('ExecuteSonarQubeReport')
{
sh "${mavenHome}/bin/mvn sonar:sonar"
}

stage('UploadArtifactIntoNexus')
{
sh "${mavenHome}/bin/mvn deploy"
}

stage('DeployAppIntoTomcatServer')
{

 
 sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.134.89.26:/opt/apache-tomcat-9.0.37/webapps/"  
}
}
