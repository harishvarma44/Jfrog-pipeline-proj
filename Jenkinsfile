node{

   def tomcatWeb = '/home/harishk/apache-tomcat-9.0.41/webapps'
   def tomcatBin = '/home/harishk/apache-tomcat-9.0.41/bin'
   def tomcatStatus = ''
   stage('SCM Checkout'){
     git 'https://github.com/harishvarma44/Jfrog-pipeline-proj.git'
   }
   stage('Compile-Package-create-war-file'){
      // Get maven home path
      def mvnHome =  tool name: 'mvn3.3.9', type: 'maven'   
      sh "${mvnHome}/bin/mvn package"
      }
/*   stage ('Stop Tomcat Server') {
               bat ''' @ECHO OFF
               wmic process list brief | find /i "tomcat" > NUL
               IF ERRORLEVEL 1 (
                    echo  Stopped
               ) ELSE (
               echo running
                  "${tomcatBin}\\shutdown.bat"
                  sleep(time:10,unit:"SECONDS") 
               )
'''
   }*/
   stage('Deploy to Tomcat'){
     sh "cp target/JenkinsWar.war ${tomcatWeb}/JenkinsWar.war"
   }
      stage ('Start Tomcat Server') {
         sleep(time:5,unit:"SECONDS") 
         bat "${tomcatBin}\\startup.sh"
         sleep(time:100,unit:"SECONDS")
   }
}
