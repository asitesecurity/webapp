pipeline {
  agent any 
  tools {
    maven 'maven'
  }
  stages {
    stage ('Initialize') {
      steps {
        sh '''
                    // echo "PATH = ${PATH}"
                  echo "PATH = ${env.PATH}"
                    echo "M2_HOME = ${M2_HOME}"
            ''' 
      }
    }
    
   
    
 
   stage ('Source Composition Analysis') {
      steps {
         sh 'rm owasp* || true'
        sh 'wget https://raw.githubusercontent.com/asitesecurity/webapp/master/owasp-dependency-check.sh'
         sh 'chmod +x owasp-dependency-check.sh '
        sh 'pwd'
        sh 'whoami'
         sh 'bash owasp-dependency-check.sh'
       //  sh 'echo "jenkins" | sudo -S -k bash owasp-dependency-check.sh'
        sh 'cat /var/lib/jenkins/OWASP-Dependency-Check/reports/dependency-check-report.xml' 
        sh 'pwd'
        
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
             sh 'pwd'
               sh 'cp target/*.war /opt/tomcat/apache/webapps/webapp.war'
             //      sh 'echo "3202de9273fe4362af50e3fdcf486ff8" | sudo -S -k cp target/*.war /opt/tomcat/apache-tomcat-8.5.81/webapps/webapp.war'
            //    sh 'sshpass -p "kali" scp -o StrictHostKeyChecking=no target/*.war kali@192.168.100.131:/opt/tomcat/apache-tomcat-8.5.81/webapps/webapp.war'
            // sh 'sshpass -p "toor" scp -o StrictHostKeyChecking=no target/*.war root@192.168.100.131:/opt/tomcat/apache-tomcat-8.5.81/webapps/webapp.war'
            // sh 'cp target/*.war /opt/tomcat/apache-tomcat-8.5.81/webapps/'
             
            // sh 'sshpass -p "kali" ssh kali@192.168.100.131 "pwd"'
              }      
           }       
    }  
}

}
