pipeline{
  agent any
   tools{
         maven "Maven"
        }
  stages{
	  stage('checkout')
	   {
	     steps{
		    git credentialsId: '15f0a019-ecce-4205-bf7b-0ddaccba1fa3', url: 'https://github.com/stpl-pro/jenkins-calculator.git'
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
