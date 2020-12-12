pipeline {
    agent any
	
	  tools
    {
       maven "Maven 3.6.3"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'main', url: 'git@github.com:Cloud-Devops-Automation/CI-CD-Docker.git'
             
          }
        }
	 stage('Execute Maven 3.6.3') {
           steps {
             
                sh 'mvn package'             
          }
        }
        

  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t samplewebapp:latest .' 
                sh 'docker tag samplewebapp thanishinfotech/samplewebapp:latest'
                //sh 'docker tag samplewebapp thanishinfotech/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
          sh  'docker push thanishinfotech/samplewebapp:latest'
        //  sh  'docker push thanishinfotech/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8083 thanishinfotech/samplewebapp"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://jenkins@172.31.28.25 run -d -p 8003:8083 thanishinfotech/samplewebapp"
 
            }
        }
    }
	}
    
