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
					sh 'docker build -t chrisvo-pipeline .'
				}
		}
		stage('Start App'){
				steps{
					sh 'docker run -dp 3000:3000 chrisvo-pipeline'
				}
		}
		stage('Install Dependencies'){
				steps{
					sh 'npm install --legacy-peer-deps xvfb'
				}
		}
		stage('Install More Dependencies'){
				steps{
					sh 'apt-get install -y libgtk2.0-0 libgtk-3-0 libgbm-dev libnotify-dev libgconf-2-4 libnss3 libxss1 libasound2 libxtst6 xauth xvfb'
				}
		}
		stage('Verify Cypress'){
				steps{
					sh 'npx cypress verify'
				}
		}
		stage('Run Tests'){
				steps{
					sh 'npm test'
				}
		}
		stage('Publish HTML Report'){
				steps{
					publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'cypress/reports/mochareports', reportFiles: 'report.html', reportName: 'HTML Report', reportTitles: ''])
				}
		}
	}
}

