pipeline {
    agent any
	
	  tools
    {
       maven "Maven"
    }
 stages {
      stage('GIT Checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/Niha-21/CI-CD-using-Docker.git'
             
          }
        }
	 stage('Execute Maven') {
           steps {
             
                bat 'mvn package'             
          }
        }
        stage('Testing Maven') {
           steps {
             
                bat 'mvn test'             
          }
        }

  stage('Docker Build and Tag') {
           steps {
              
                bat 'docker build -t webapp:latest .' 
                bat 'docker tag webapp nihak/webapp:latest'
                //sh 'docker tag samplewebapp nikhilnidhi/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish Image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "docker-hub", url: "https://registry.hub.docker.com" ]) {
          bat  'docker push nihak/webapp:latest'
        //  sh  'docker push nikhilnidhi/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker Container on Jenkins Agent') {
             
            steps 
			{
                bat "docker run -d -p 9093:8080 nihak/webapp"
 
            }
        }
 stage('Run Docker Container on Remote Hosts') {
             
            steps {
                bat "docker -H ssh://deployer@localhost:8081 run -d -p 9093:8080 nihak/webapp"
 
            }
        }
    }
	}
    
