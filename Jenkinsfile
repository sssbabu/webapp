pipeline{
 tools{
        jdk 'JAVA_HOME'
        maven 'M2_HOME'
    }
     agent any
	  
	  stages{
	  
	  stage("checkout"){
	   steps{
	   git 'https://github.com/nishankainfo/webapp.git'
	   }
	                  }
	
	   stage("compile"){
	    steps{
		 sh 'mvn compile'
		}
		}
       stage("test"){
	    steps{
		 sh 'mvn test'
		}
		}
       stage("package"){
	    steps{
		 sh 'mvn clean package'
                 sh "mv target/*.war target/myweb.war"

		}
		}
   
		  stage("nexus"){
	    steps{
		 nexusArtifactUploader artifacts: [[artifactId: 'idream-it-solutions', classifier: '', file: 'target/idream-it-solutions-1.0.war', type: 'war']], credentialsId: 'nexus', groupId: 'com.idream.webapp', nexusUrl: '13.233.141.181:8080/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'http://13.233.141.181:8080/nexus/content/repositories/repoR/', version: '1.0'

		}
		}
		  
      stage("deploy"){
	    steps{
		 sshagent(['myjenkins']) {
            

                  sh """
                 
            scp -o StrictHostKeyChecking=no target/myweb.war ec2-user@15.206.149.50:/home/ec2-user/tomcat8/webapps/

              ssh ec2-user@15.206.149.50 /home/ec2-user/tomcat8/bin/shutdown.sh
               ssh ec2-user@15.206.149.50 /home/ec2-user/tomcat8/bin/startup.sh
            
          
          """



    // some block
}
		}
		}
	  }
	}
