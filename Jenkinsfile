pipeline {
    agent any
    stages {
        stage('SCM') {
            steps {
                git url: 'https://github.com/GnitkoPavel/helloworld.git'
            }
        }
        stage('build && SonarQube analysis') {
            steps {
                withSonarQubeEnv('My SonarQube Server') {
                    // Optionally use a Maven environment you've configured already
                    withMaven(maven:'Maven 3.0.5') {
                        sh 'mvn clean sonar:sonar   -Dsonar.host.url=http://192.168.60.4:9000/sonar   -Dsonar.login=36ab12c6b71e36761e41953e98086f71893c2daf'
                    }
                }
            }
        }
        
    }
}
