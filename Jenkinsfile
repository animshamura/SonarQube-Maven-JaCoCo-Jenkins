pipeline {
    agent any
    tools {
        jdk 'JDK'
        maven 'Maven'
    }
    environment {
        SCANNER_HOME=tool 'Sonar'
    }
    stages {
        stage('Git Check') {
            steps {
               git branch: 'main', url: 'https://github.com/spring-projects/spring-petclinic.git'
            }
        }
         stage('Compile Code') {
            steps {
                sh "mvn clean compile"
            }
        }
        stage('Code Test') {
            steps {
                sh "mvn test"
            }
        }
        stage('Sonar Analysis') {
            steps {
                 withSonarQubeEnv('Sonar') {
                    sh "mvn clean verify sonar:sonar \
                       -Dsonar.projectKey=losbe \
                       -Dsonar.host.url=http://172.17.18.200:9000 \
                       -Dsonar.login=sqp_e3889c34f177722866048517b799ebff4be607fc
                }
            }
        }
    }
}
