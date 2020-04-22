pipeline {
    
  agent { 
      label 'master'
      }
   tools {
      // Install the Maven version configured as "M3" and add it to the path.
      maven "maven3"
   }

   stages {
      stage('getscm') {
         steps {
            
               git  'https://github.com/jmstechhome6/spring3-mvc-maven-xml-hello-world.git'     
         }
      }
      stage('build'){
          steps{
             sh "mvn -Dmaven.test.failure.ignore=true clean package"
             }
          }
      stage('artifact'){
          steps{
                 archiveArtifacts 'target/*.war'
         }
      }
      stage('deploy') {
             steps{
                 
                  withCredentials([usernameColonPassword(credentialsId: 'tomcat_credentials', variable: 'tomcat_secrets')]) 
                    {
                      sh "curl  -u ${tomcat_secrets} -T /var/lib/jenkins/workspace/mvn_pipeline/target/spring3-mvc-maven-xml-hello-world-1.0-SNAPSHOT.war 'http://ec2-52-66-154-23.ap-south-1.compute.amazonaws.com:8081/manager/text/deploy?path=/jenkins_deploy&update=true'"
                    }              
                     
                 
             }
             }
         }
}
   
