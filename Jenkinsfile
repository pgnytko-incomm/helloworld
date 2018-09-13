pipeline {
    agent any
    stages {
        stage('SCM') {
            steps {
                git url: 'https://github.com/GnitkoPavel/helloworld.git'
            }
        }
        stage('Sonarqube') {
          environment {
            scannerHome = tool 'SonarQubeScanner'
          }
          steps {
            withSonarQubeEnv('sonarqube') {
              sh "/opt/sonar-scanner/bin/sonar-scanner"
           }
            timeout(time: 30, unit: 'SECONDS') {
              waitForQualityGate abortPipeline: true
           }
          }
        }
        stage('Unit testing') {
            steps {
              sh "mvn test"
            
            }
        
        
        }
        stage('Notofocation') {
            emailext (
            subject: "STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
            body: """<p>STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
              <p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>""",
            recipientProviders: [[$class: 'DevelopersRecipientProvider']]
          )
        }
    }
}
