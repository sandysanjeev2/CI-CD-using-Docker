pipeline {
    agent any
	
	
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/sandysanjeev2/CI-CD-using-Docker.git'
             
          }
        }
	 stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
        

  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t samplewebapp:latest .' 
                sh 'docker tag samplewebapp sandysanjeev2/samplewebapp:latest'
                //sh 'docker tag samplewebapp sandysanjeev2/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
          sh 'docker login -u sandysanjeev2 --password-stdin 12671aA0345$'
		sh  'docker push sandysanjeev2/samplewebapp:latest'
        //  sh  'docker push sandysanjeev2/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 sandysanjeev2/samplewebapp"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://jenkins@172.31.28.25 run -d -p 8003:8080 sandysanjeev2/samplewebapp"
 
            }
        }
    }
	}
    
