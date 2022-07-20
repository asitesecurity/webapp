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
    
    
   /* stage ('Source Composition Analysis') {
      steps {
         sh 'rm owasp* || true'
         sh 'wget "https://raw.githubusercontent.com/asitesecurity/webapp/master/owasp-dependency-check.sh" '
         sh 'chmod +x owasp-dependency-check.sh'
         sh 'bash owasp-dependency-check.sh'
         sh 'cat /var/lib/jenkins/OWASP-Dependency-Check/reports/dependency-check-report.xml'
        
      }
    }
    
    */
    
    stage ('Build') {
      steps {
      sh 'mvn clean package'
            }
          }


stage ('Deploy-To-Tomcat') {
            steps {
           sshagent(['tomcat']) {
                sh 'sshpass -p "kali" scp -o StrictHostKeyChecking=no target/*.war kali@192.168.100.131:/opt/tomcat/apache-tomcat-8.5.81/webapps/webapp.war'
            // sh 'sshpass -p "toor" scp -o StrictHostKeyChecking=no target/*.war root@192.168.100.131:/opt/tomcat/apache-tomcat-8.5.81/webapps/webapp.war'
            // sh 'cp target/*.war /opt/tomcat/apache-tomcat-8.5.81/webapps/'
             
             sh 'sshpass -p "kali" ssh mkdir kali@192.168.100.131:/opt/tomcat/apache-tomcat-8.5.81/webapps/test123.txt'
              }      
           }       
    } 
}

}
