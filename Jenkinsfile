pipeline {
  agent any
  stages {

    stage('Docker build and push') {
      steps {
		sh '''
		 whoami
		 #aws configure set aws_access_key_id $ACCESS_KEY
		 #aws configure set aws_secret_access_key $ACCESS_SECRET_KEY
		 #aws configure set default.region ap-southeast-1
		 aws ecr get-login-password --region ap-southeast-1 | docker login --username AWS --password-stdin 933542948767.dkr.ecr.ap-southeast-1.amazonaws.com
		 docker build -t docker1 .
		 docker tag docker1:latest 933542948767.dkr.ecr.ap-southeast-1.amazonaws.com/docker1:${BUILD_NUMBER}
		 docker push 933542948767.dkr.ecr.ap-southeast-1.amazonaws.com/docker1:${BUILD_NUMBER}
		  '''
	     }	         
	   }

    stage('Deploy docker'){
      steps {
		sh '''
			  ssh -i /var/lib/jenkins/.ssh/application.pem -o StrictHostKeyChecking=no ubuntu@ec2-54-180-134-105.ap-northeast-2.compute.amazonaws.com 'bash -s' < ./deploy.sh \${BUILD_NUMBER}
			  '''	 
		    
      		}
		}		    

}

 }
