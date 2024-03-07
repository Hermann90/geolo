pipeline {
    triggers {
  pollSCM('* * * * *')
    }
   agent any
    tools {
  maven 'M2_HOME'
  jfrog 'Jfrog remote cli'
}

    stages {

        stage('maven package') {
            steps {
                sh 'mvn clean'
                sh 'mvn package -DskipTests'
                sh 'ls target'
            }
        }
        stage('PUSH JFROG') {
            
            steps {
                script{
                    // install pipeline-utility-steps plugin for the ReadMavenPom method
                    def mavenPom = readMavenPom file: 'pom.xml'
                    POM_VERSION = "${mavenPom.version}"
                    APP_NAME = "${mavenPom.name}"
                    echo "${POM_VERSION}"
                    echo "${APP_NAME}"
                    sh "curl -uadmin:AP77hxSx85EFzMRQD9h9k5NQR1N -T target/${APP_NAME}-${POM_VERSION}.jar http://172.234.203.14:8081/artifactory/geolocation/${POM_VERSION}/${APP_NAME}-${POM_VERSION}.jar"
                } 
            }
        }    	    
    }
}