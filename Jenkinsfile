pipeline{
 tools{
        jdk 'JAVA_HOME'
        maven 'M2_HOME'
    }
     agent any
	  
	  stages{
	  
	  stage("checkout"){
	   steps{
	   git 'https://github.com/BikashPanda1998/webapp.git'
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
   stage("deploy"){
	   steps{

     sshagent(['tomcat_user']) {
    // some block

	        sh """
                 
            scp -o StrictHostKeyChecking=no target/myweb.war ec2-user@13.235.81.207:/home/ec2-user/tomcat8/webapps/

              ssh ec2-user@13.235.81.207 /home/ec2-user/tomcat8/bin/shutdown.sh
               ssh ec2-user@13.235.81.207 /home/ec2-user/tomcat8/bin/startup.sh
            
          
          """

}

	   
		}
		  
	  }


	}
}
