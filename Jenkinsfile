pipeline{
  agent any
   tools{
         maven "Maven"
        }
  stages{
	  stage('checkout')
	   {
	     steps{
		    git branch: 'dev', credentialsId: '65b54889-a611-4ec5-9c31-594d2b0993cf', url: 'https://github.com/Ki5h/taxi-booking.git'
     		  }
           }
          stage('Build')
           {
             steps{
                    sh "mvn clean package"
                  }

	   }
          stage('test')
           {
             steps{
                    sh "mvn clean sonar:sonar"
                  }
           }
         stage('upload to nexus')
           {
             steps{
                    sh "mvn clean deploy"
                  }
           }
         stage('Deploy to tomcat')
           {
             steps{ 
             sshagent(['d07dc9a1-6bf6-43a3-959f-4a1ff85bb779']) 
              {
               sh "scp -o StrictHostKeyChecking=no target/calculator.war ec2-user@54.145.189.62:/usr/share/apache-tomcat-9.0.63/webapps/"
              }
                }
           }
    }
}
