pipeline {
    agent any

    stages {
        stage('Code Quality ') {
            steps {
                echo 'sonaranalysis started'
                sh 'cd webapp && sudo docker run  --rm -e SONAR_HOST_URL="http://3.89.224.107:9000" -e SONAR_LOGIN="sqp_4a8b96d2bd597481d30e658fc8709215a8c01613"  -v ".:/usr/src" sonarsource/sonar-scanner-cli:5.0 -Dsonar.projectKey=lms'
                echo 'Sonar Analysis Completed'
            }
        }
        stage('Built LMS') {
            steps {
                echo 'LMS build started'
                sh 'cd webapp && npm install && npm run build'
                echo 'LMS build Completed'
            }
        }
        stage('Publish LMS') {
            steps {
                script {
            def packageJson = readJSON file: 'webapp/package.json'
            def packageJsonVersion = packageJson.version
            echo "${packageJsonVersion}"
            sh "zip webapp/lms-${packageJsonVersion}.zip -r webapp/dist"
            sh "curl -v -u admin:admin@123 --upload-file webapp/lms-${packageJsonVersion}.zip http://3.89.224.107:8081/repository/lms/"
         }
            }
        }
        stage('Deploy LMS') {
            steps {
                script {
            def packageJson = readJSON file: 'webapp/package.json'
            def packageJsonVersion = packageJson.version
            echo "${packageJsonVersion}"
            sh "curl -u admin:admin@123 -X GET \'http://3.89.224.107:8081/repository/lms/lms-${packageJSONVersion}.zip\' --output lms-'${packageJSONVersion}'.zip"
            sh 'sudo rm -rf /var/www/html/*'
            sh "sudo unzip -o lms-'${packageJSONVersion}'.zip"
            sh "sudo cp -r webapp/dist/* /var/www/html"
        

            }
        }
    }

       stage('Clean Up Workspace') {
           steps {
                   echo 'Cleaning Work Space'
                   // Install Cleanup Workspace plugin to make below command work
                   cleanWs()
           }
       }
    }
}