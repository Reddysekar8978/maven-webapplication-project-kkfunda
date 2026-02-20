node
{

   echo "git branch name: ${env.BRANCH_NAME}"
   echo "build number is: ${env.BUILD_NUMBER}"
   echo "node name is: ${env.NODE_NAME}"


   // /var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/maven_6/bin
   def mavenHome=tool name: "maven 6"
   

  stage('git checkout')
  {
    notifyBuild('STARTED')
    git branch: 'dev2', url: 'https://github.com/Reddysekar8978/maven-webapplication-project-kkfunda.git'
  } 

    stage('COMPILE')
  {
    sh "${mavenHome}/bin/mvn clean compile"
  }

  stage('Build')
  {
    sh "${mavenHome}/bin/mvn clean package"
  }

    stage('SQ Report')
  {
    sh "${mavenHome}/bin/mvn sonar:sonar"
  }

      stage('Upload Artifact')
  {

    sh "${mavenHome}/bin/mvn clean deploy"
  }

    stage('Deploy to Tomcat') 
    {
      
      sh """

      curl -u sekhar:sekhar \
       --upload-file /var/lib/jenkins/workspace/jio-scripted-way-PL/target/maven-web-application.war \
       "http://13.235.99.80:8080/manager/text/deploy?path=/maven-web-application&update=true"
          
        """
    }

    }  
  


  
