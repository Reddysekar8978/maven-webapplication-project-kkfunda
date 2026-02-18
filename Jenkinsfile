node
{

// /var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/maven_6/bin

def mavenHome=tool name: "maven 6"
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
 curl -u sekar:sekar \
--upload-file /var/lib/jenkins/workspace/jio-scriptedway/target/maven-web-application.war \
http://13.235.99.80:8080//"manager/text/deploy?path=/maven-web-application&update=true"
          
        """
}
}
