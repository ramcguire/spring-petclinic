pipeline {
    agent any
    environment {
      ARTIFACTORY_CREDS = credentials('Artifactory')
    }
    stages {
        stage ('Compile') {
            steps {
                sh 'mvn -s /usr/share/java/maven-3/conf/settings.xml compile'
            }
        }

        stage ('Test') {
          steps {
              sh 'mvn -s /usr/share/java/maven-3/conf/settings.xml test'
          }
        }

        stage ('Package') {
          steps {
              sh 'mvn -s /usr/share/java/maven-3/conf/settings.xml package'
          }
        }

        stage ('Deploy') {
            steps { 
              pwd && sh 'curl -u $ARTIFACTORY_CREDS -X PUT "http://localhost:8081/artifactory/libs-snapshot/spring-petclinic-pipeline/spring-petclinic-pipeline.war" -T target/petclinic-pipeline.war'
            }
        }
    }
}