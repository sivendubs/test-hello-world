pipeline {
    agent any
    tools {
        maven 'Maven' 
    }
    stages {
       stage('Build') {
      		steps {
	    		script {
	    			LAST_STARTED = env.STAGE_NAME
				sh "mvn clean install  -DskipTests"     
				
		        } 
              }    
     } 
     stage ('Munit Test'){
        	steps {
			script {
			    LAST_STARTED = env.STAGE_NAME
			   	sh "mvn test"
				publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'target/site/munit/coverage', reportFiles: 'summary.html', reportName: 'Munit HTML Report', reportTitles: ''])
				}	
			}		
          
     }
  
    stage('Deploy to Cloudhub'){
        	steps {
			script {
			    LAST_STARTED = env.STAGE_NAME
				sh 'mvn package deploy -DmuleDeploy -DskipTests -Danypoint.username=sivendu07 -Danypoint.password=Sivendu@903 -DapplicationName=hello-world-njclabs '
			    }
       }
   }
   
    }  
   }
