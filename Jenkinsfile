pipeline {
    agent any

    stages {
        stage('preparation') {
            steps {
                git 'https://github.com/montaser223/Booster_CI_CD_Project'
            }
        }
        stage('CI') {
            steps {
                sh 'docker build . -t montaser/django_cicd:1.0'
            }
        }
        stage('CD') {
            steps {
                sh 'docker run -d -p 8000:8000 montaser/django_cicd:1.0'
            }
            
            post{
            	success{
            		slackSend (color:"#dddddd", message: "CICD cycle completed successfully")
            	}
            }
        }
        
    }
}

