
pipeline {

	agent any
  tools 
  { nodejs '16.10.0' }  
  
	stages {
		
		stage('Git ') {
            steps {
                echo 'pulling Main Project from git ...';
                git branch: 'main', credentialsId: 'git', url: 'https://github.com/amineturki/projet-cd.git'            }
        }
    
 /*      stage('Docker Build and Push') {
       steps {
         withDockerRegistry([credentialsId: "docker-hub", url: ""]) {
           sh 'sudo docker build -t amineturki/cd:latest .'
           sh 'docker push amineturki/cd:latest '
         }
       }
     }
	 */
	 	stage('Ansible playbook for test') {
            steps {
               sh 'echo $PATH'
               sh 'ng version'
                sh 'ansible-playbook playbook-test.yml'
                         }
        }
     	
    


 

 stage('Ansible playbook for building the app') {
            steps {
                sh 'ansible-playbook ansible/build.yml -i ansible/inventory/hosts.yml'
                         }
        }
    
    stage('Ansible playbook for building the image and running the container') {
            steps {
                sh 'ansible-playbook ansible/docker.yml -i ansible/inventory/hosts.yml'
                         }
        }
        stage('Ansible playbook for pushing the image to a dockerhub repository') {
            steps {
                sh 'ansible-playbook ansible/docker-registry.yml -i ansible/inventory/hosts.yml'
                         }
        }

	 
	}
	}
