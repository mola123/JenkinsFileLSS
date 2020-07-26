node
{
def mavenHome = tool name: "Maven3.6.3"
stage ('get code')
{
git branch: 'development', credentialsId: 'gitCredentials', url: 'https://github.com/mylandmarktech/maven-web-application.git'
}
stage ('Build')
{
sh "${mavenHome}/bin/mvn clean package"
}
stage ('sonar')
{
sh "${mavenHome}/bin/mvn sonar:sonar"
}
stage ('NexusUpload')
{
sh "${mavenHome}/bin/mvn deploy"
}
stage('DeployAppIntoTomcatServer')
{
 sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.134.89.26:/opt/apache-tomcat-9.0.37/webapps/"  
}
stage ('email notification')
{
emailext body: '''Deploy successesful
Regards
Landmark Technologies''', subject: 'Success', to: 'mylandmarktech@gmail.com'
}
}
