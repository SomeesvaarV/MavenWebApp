pipeline{
	agent any
	environment{
		LANG = 'en_US.UTF-8'
		LC_ALL = 'en_US.UTF-8'
	}
	tools{
		maven 'Maven'
	}
	
	stages{
		stage('Checkout'){
			steps{
				git branch:'main', url:'https://github.com/SomeesvaarV/MavenWebApp.git'
			}
		}
		stage('Build'){
			steps{
				sh 'mvn clean package' 
			}
		}
		stage('Archive'){
			steps{
				archiveArtifacts artifacts: 'target/*.war', fingerprint:true 
			}
		}
		stage('Deploy'){
			steps{
				sh 'mvn clean package'
				sh 'ansible-playbook ansible/playbook.yml -i ansible/hosts.ini' 
			}
		}
	}
	
	post{
		success{
			echo 'Build and Deployment Successful'
		}
		failure{
			echo 'Builed failed'
		}
	}
}
