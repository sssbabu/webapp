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
		 sh 'mvn package'
                 sh "mv target/*.war target/myweb.war"

		}
		}
      stage("deploy"){
	    steps{
		 sshagent(['myjenkins']) {
            

                  sh """
                 
            scp -o StrictHostKeyChecking=no target/myweb.war ec2-user@15.206.149.50:/home/ec2-user/tomcat8/webapps/

              ssh ec2-user@15.206.149.50 /home/ec2-user/tomcat8/bin/shutdown.sh
               ssh ec2-user@15.206.149.50 /home/ec2-user/tomcat8/bin/startup.sh
             chmod -R 777 webapps temp logs work conf
             chmod -R 777 tomcat8 
          
          """



    // some block
}
		}
		}
	  }
	}
