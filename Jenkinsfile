pipeline {
agent any
    environment {
   	 PROJECT_ID = 'lab3cit'
            	CLUSTER_NAME = 'lab-3-cluster'
            	LOCATION = 'europe-central2'
            	CREDENTIALS_ID = 'kubernetes'
    }
    stages {
    	stage('Checkout') {
   	 	steps {
   		 	checkout scm
   	 	}
    	}
    	stage('Build image') {
   	 	steps {
   		 	script {
   			 	app = docker.build("zetzo/pipeline:${env.BUILD_ID}")
   		  	}
   						 	 
   	 	}
    	}
       	stage('Deploy to K8s') {
   	 	steps{
   		 	echo "Deployment started ..."
   		 	sh 'ls -ltr'
   		 	sh 'pwd'
   		 	step([
    $class: 'KubernetesEngineBuilder',
    projectId: env.PROJECT_ID,
    clusterName: env.CLUSTER_NAME,
    location: env.LOCATION,
    manifestPattern: 'deployment.yaml',
    credentialsId: env.CREDENTIALS_ID,
    verifyDeployments: true
])
   			 }
   		 }
   	 }    
}
