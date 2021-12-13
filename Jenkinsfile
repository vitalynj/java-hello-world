pipeline {
    agent any
    tools {
        maven 'maven'
        jdk 'jdk8'
          }
    stages {
        stage('GitHub clone stage') {
            steps {
                echo "******************** Copying code from GitHub started ********************"
                git branch: 'main',
                url: 'https://github.com/vitalynj/java-hello-world.git'
                checkout scm
                echo "******************** Copying code from GitHub ********************"
            }
        }
        stage('Build code stage') {
            steps {
                echo "******************** Building the code ********************"
                sh 'mvn package -DskipTests=false'
            }
        }
        stage('Sonar scan stage') {
            tools{
                jdk 'jdk11'
            }
        steps {
            withSonarQubeEnv(installationName: 'SonarQube') {
            sh '''
                echo "******************** Sonar scan ********************"
                mvn sonar:sonar \
                -Dsonar.projectKey=Jenkins \
                -Dsonar.host.url=http://172.17.0.3:9000 \
                -Dsonar.login=11a83365b2b4e9e40e1e520154452a2a638af23f
            '''  
            }
        }
        }
    }
}
