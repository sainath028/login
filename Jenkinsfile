pipeline {
    agent any
	
    tools {
        nodejs "node_v10"
        maven "maven"
    }
    
    stages {
        stage ('PULL CODE') {            
            steps {
                dir('ui') {
                    git branch: 'master', credentialsId: 'sainath', url: 'https://sainathkadaverugu@bitbucket.org/ui.git'
                }
               
                dir('api') {
                    git branch: 'master', credentialsId: 'sainath', url: 'https://sainathkadaverugu@bitbucket.org/api.git'
                }
            }
        }

        stage ('build UI CODE') {
            steps {
                dir('ui') {
                 sh 'npm install'
                
                }
            }
        }
        
        stage ('Copy content from UI to api') {
            steps {
                sh 'cp -Rp ui/dist/* api/src/main/resources/static/'
            }
        }
        
       stage ('build api'){
           steps {
               dir('api') {
                   sh 'mvn clean install'
               }
           }
       }
        
        stage ('Deploy Tomcat') {
    	    steps {
    		    dir('api') {
                    deploy tomcat script
       			}
      		}
        	}
        }
        
    }
}
