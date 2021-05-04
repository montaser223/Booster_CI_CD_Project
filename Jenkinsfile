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
                withCredentials([usernamePassword(credentialsId: 'docker', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
                
                    sh """
                    docker build . -t montaser98/django_jen
                    docker login --username ${USERNAME} --password ${PASSWORD}
                    docker push montaser98/django_jen
                    """
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

