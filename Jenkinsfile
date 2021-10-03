pipeline {
	agent any
	
	tools {nodejs "nodejs"}
	
	stages {
		stage('Clone Git Repo'){
				steps{
					git 'https://github.com/ChrisVo0505/todo-cypress-jenkins-docker.git'
		    }
		}
		stage('Build App'){
				steps{
					bat 'docker build -t chrisvo-pipeline .'
				}
		}
		stage('Start App'){
				steps{
					bat 'docker run -dp 3000:3000 chrisvo-pipeline'
				}
		}
		stage('Install Dependencies'){
				steps{
					bat 'npm install --legacy-peer-deps xvfb'
				}
		}
		stage('Install More Dependencies'){
				steps{
					bat 'apt-get install -y libgtk2.0-0 libgtk-3-0 libgbm-dev libnotify-dev libgconf-2-4 libnss3 libxss1 libasound2 libxtst6 xauth xvfb'
				}
		}
		stage('Verify Cypress'){
				steps{
					bat 'npx cypress verify'
				}
		}
		stage('Run Tests'){
				steps{
					bat 'npm test'
				}
		}
		stage('Publish HTML Report'){
				steps{
					publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'cypress/reports/mochareports', reportFiles: 'report.html', reportName: 'HTML Report', reportTitles: ''])
				}
		}
	}
}

