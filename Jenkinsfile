pipeline {
    agent any
     tools {
        maven 'Maven' 
        }
    stages {
        stage("Test"){
            steps{
                // mvn test
                sh "mvn test"                
            }
        }
        stage("Build"){
            steps{
                sh "mvn package"   
            }
        }
        stage("Deploy on Test"){
            steps{
                // deploy on container -> plugin
                deploy adapters: [tomcat9(credentialsId: 'tomcatserverdetails1', path: '', url: 'http://13.233.139.65:8080')], contextPath: '/app', war: '**/*.war' 
            }
        }
        stage("Deploy on Prod"){
             input {
                message "Should we continue?"
                ok "Yes we Should"
            }
            steps{
                // deploy on container -> plugin
                deploy adapters: [tomcat9(credentialsId: 'tomcatserverdetails1', path: '', url: 'http://3.110.43.211:8080')], contextPath: '/app', war: '**/*.war'
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
             slackSend channel: 'youtubejenkins', message: 'Success'
        }
        failure{
            echo "========pipeline execution failed========"
             slackSend channel: 'youtubejenkins', message: 'Job Failed'
        }
    }
}
