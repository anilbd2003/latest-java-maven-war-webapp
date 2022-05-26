pipeline {
  agent any
  tools {
    maven 'Maven'
 
  }

  stages{
    stage('Initialize'){
      steps {
      sh '''
          echo "PATH=${PATH}"
          echo "M2_HOME= ${M2_HOME}"
          '''
      }
    }  
    stage('Build') {
      steps {
        sh 'mvn clean package'
        }
     }
    stage('deploy to tomcat') {
      steps {
        sshagent(['tomcat']) {
          sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@{tomcatpubIP}:/prod/apache-tomcat-8.5.78/webapps/webapp.war'
        }
      
      }
  }
  }
}
