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
    
    
   stage ('Source Composition Analysis') {
      steps {
         sh 'sshpass -p "kali" ssh kali@192.168.100.131 "rm owasp* || true"'
         sh 'sshpass -p "kali" ssh kali@192.168.100.131 "wget https://raw.githubusercontent.com/asitesecurity/webapp/master/owasp-dependency-check.sh" '
         sh 'sshpass -p "kali" ssh kali@192.168.100.131 "chmod +x owasp-dependency-check.sh" '
         sh 'sshpass -p "kali" ssh kali@192.168.100.131 "bash owasp-dependency-check.sh" '
         sh 'sshpass -p "kali" ssh kali@192.168.100.131 "cat /var/lib/jenkins/OWASP-Dependency-Check/reports/dependency-check-report.xml" ' 
        sh 'sshpass -p "kali" ssh kali@192.168.100.131 "pwd"'
        
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
                sh 'sshpass -p "kali" scp -o StrictHostKeyChecking=no target/*.war kali@192.168.100.131:/opt/tomcat/apache-tomcat-8.5.81/webapps/webapp.war'
            // sh 'sshpass -p "toor" scp -o StrictHostKeyChecking=no target/*.war root@192.168.100.131:/opt/tomcat/apache-tomcat-8.5.81/webapps/webapp.war'
            // sh 'cp target/*.war /opt/tomcat/apache-tomcat-8.5.81/webapps/'
             
            // sh 'sshpass -p "kali" ssh kali@192.168.100.131 "pwd"'
              }      
           }       
    } 
}

}
