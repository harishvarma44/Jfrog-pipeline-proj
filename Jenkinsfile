pipeline {
    agent any
    environment{
        PATH= "/usr/share/maven/bin:$PATH"
        def tomcatWeb = '/home/harishk/apache-tomcat-9.0.41/webapps'
        def tomcatBin = '/home/harishk/apache-tomcat-9.0.41/bin'

    }
    stages {
        stage('SCM Checkout') {
            steps{
               git credentialsId: 'git_credentials', url: 'https://github.com/harishvarma44/Jfrog-pipeline-proj.git'
                 }
            }
        stage('Build-Code') {
            steps {
                //   def mvnHome =  tool name: 'mvn3.3.9', type: 'maven'
                   sh "mvn clean package"
                  }
            }

        stage('Testing Phase') {
            steps {
               sh 'mvn test'
           }
//            post {
//                always {
//                    junit 'target/superfire-reports/*.xml'
//                }
//            }
        }

        stage('Deploy Tom') {
            steps {
                sshagent(['jenkins1-slave']) {
                  sh "scp -o StrictHostKeyChecking=no target/JenkinsWar.war harishk@192.168.161.7:${tomcatWeb}/jenkinsWar.war"
            }
        }
      }
  }

}

