pipeline {
  agent any 
  tools {
    maven 'maven'
  }
  stages {
    stage ('Initialize') {
      steps {
        sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
            ''' 
      }
    }
    
    
    
    stage ('Build') {
      steps {
      sh 'mvn clean package'
            }
          }


stage ('Deploy-To-Tomcat') {
            steps {
           sshagent(['tomcat']) {
                sh 'scp -o StrictHostKeyChecking=no target/*.war root@192.168.100.131:/opt/tomcat/apache-tomcat-8.5.81/webapps/webapp.war'
            // sh 'sshpass -p "toor" scp -o StrictHostKeyChecking=no target/*.war root@192.168.100.131:/opt/tomcat/apache-tomcat-8.5.81/webapps/webapp.war'
            // sh 'cp target/*.war /opt/tomcat/apache-tomcat-8.5.81/webapps/'
              }      
           }       
    } 
}

}
