pipeline {
    agent any
    tools {
        maven 'maven'
        jdk 'jdk8'
          }
    stages {
        stage('Clone code from GitHub') {
            steps {
                echo "--------------- Clone code from GitHub ---------------"
                git branch: 'master',
                url: 'https://github.com/neprosnulsea/maven-hello-world.git'
                checkout scm  
            }
        }
        stage('Build the code') {
            steps {
                echo "--------------- Build the code ---------------"
                sh 'mvn package -DskipTests=false'
            }
        }
        stage('Scan the code via Sonar') {
            tools{
                jdk 'jdk11'
            }
        steps {
            withSonarQubeEnv(installationName: 'SonarQube') {
            sh '''
                echo "--------------- Scan the code via Sonar ---------------"
                mvn sonar:sonar \
                -Dsonar.projectKey=Jenkins \
                -Dsonar.host.url=http://192.168.0.20:9000 \
                -Dsonar.login=11a83365b2b4e9e40e1e520154452a2a638af23f
                -Dsonar.sources=. \
                -Dsonar.java.binaries=. \
                -Dsonar.projectVersion=$BUILD_NUMBER
            
            '''  
            }
        }
        }
    }
}
