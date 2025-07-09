pipeline {
    agent any

    stages {
        stage('Code Quality ') {
            steps {
                sh 'sleep 10'
                echo 'Sonar Analysis Completed'
            }
        }
        stage('Built LMS') {
            steps {
                sh 'sleep 10'
                echo 'LMS builf Completed'
            }
        }
        stage('Publish LMS') {
            steps {
                sh 'sleep 10'
                echo 'Upload Artefact to Nexus'
            }
        }
        stage('Deploy LMS') {
            steps {
                sh 'sleep 10'
                echo 'LMS App Deployed'
            }
        }
    }
}
