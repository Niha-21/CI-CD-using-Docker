pipeline {
    agent any
	
	  tools
    {
       maven "Maven"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/Niha-21/CI-CD-using-Docker.git'
             
          }
        }
	 stage('Execute Maven') {
           steps {
             
                bat 'mvn package'             
          }
        }
        

  stage('Docker Build and Tag') {
           steps {
              
                bat 'docker build -t webapp:latest .' 
                bat 'docker tag webapp nihak/webapp:latest'
                //sh 'docker tag samplewebapp nikhilnidhi/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "docker-hub", url: "https://registry.hub.docker.com" ]) {
          bat  'docker push nihak/webapp:latest'
        //  sh  'docker push nikhilnidhi/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                bat "docker run -d -p 8082:8082 nihak/webapp"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                bat "docker -H ssh://jenkins@172.31.28.25 run -d -p 8082:8080 nihak/webapp"
 
            }
        }
    }
	}
    
