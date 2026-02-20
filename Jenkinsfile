node
{

// /var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/maven_6/bin

 
def mavenHome=tool name: "maven 6"
 try
 {
  notifyBuild('STARTED')
stage ('git checkout')
{
git branch: 'dev2', url: 'https://github.com/Reddysekar8978/maven-webapplication-project-kkfunda.git'
}
 stage ( 'mvn build')
{
sh "${mavenHome}/bin/mvn clean package"
}
stage('SQ Report')
{
sh "${mavenHome}/bin/mvn sonar:sonar"

}
stage (' nexus ')
{
sh "${mavenHome}/bin/mvn deploy"
} 
stage ('deploy to tomcat')
{
sh """
 curl -u sekhar:sekhar \
--upload-file /var/lib/jenkins/workspace/jio-scriptedway/target/maven-web-application.war \
http://13.235.99.80:8080//"manager/text/deploy?path=/maven-web-application&update=true"
          
        """
}
 } //Tryend
 catch (e)
 {
  currentBuild.result = "FAILED"
 }
 finally //always-sends notifications
 {
  notifyBuild(currentBuild.result)
 }
} // Node ending


def notifyBuild(String buildStatus = 'STARTED') {
  // build status of null means successful
  buildStatus =  buildStatus ?: 'SUCCESS'

  // Default values
  def colorName = 'RED'
  def colorCode = '#FF0000'
  def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
  def summary = "${subject} (${env.BUILD_URL})"

  // Override default values based on build status
  if (buildStatus == 'STARTED') {
    color = 'YELLOW'
    colorCode = '#FFFF00'
  } else if (buildStatus == 'SUCCESS') {
    color = 'GREEN'
    colorCode = '#00FF00'
  } else {
    color = 'RED'
    colorCode = '#FF0000'
  }

  // Send notifications
  slackSend (color: colorCode, message: summary, channel: '#jio-dev')
  
}
