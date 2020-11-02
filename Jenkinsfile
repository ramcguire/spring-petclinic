pipeline {
    agent any
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
                rtServer (
                    id: "ARTIFACTORY_SERVER",
                    url: "http://artifactory:8082/artifactory",
                    credentialsId: 'Artifactory'
                )
                rtUpload (
                  serverId: "ARTIFACTORY_SERVER",
                  spec: '''{
                    "files": [
                      {
                        "pattern": "spring-petclinic*.pom",
                        "target": "libs-snapshot/spring-petclinic/"
                      }
                      {
                        "pattern": "spring-petclinic*.war",
                        "target": "libs-snapshot/spring-petclinic/"
                      }
                    ]
                  }''',
                )

            }
        }

        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "ARTIFACTORY_SERVER"
                )
            }
        }
    }
}