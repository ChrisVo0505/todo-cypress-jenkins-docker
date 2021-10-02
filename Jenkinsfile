pipeline {
	agent any
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
					bat 'npm install'
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

