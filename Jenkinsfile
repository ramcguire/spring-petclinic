pipeline {
    agent any
    tools {
      maven 'Maven 3'
    }
    // environment {
    //   ARTIFACTORY_CREDS = credentials('Artifactory')
    // }
    stages {
        stage ('Get working directory') {
          steps {
            sh 'pwd'
          }
        }
        stage ('Compile') {
            steps {
                sh 'mvn compile'
            }
        }

        stage ('Test') {
          steps {
              sh 'mvn test'
          }
        }

        stage ('Package') {
          steps {
              sh 'mvn package'
          }
        }
    }
}