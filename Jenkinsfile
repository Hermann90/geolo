pipeline {
    triggers {
  pollSCM('* * * * *')
    }
   agent any
    tools {
  maven 'M2_HOME'
  jfrog 'Jfrog remote cli'
}
environment {
    registry = '076892551558.dkr.ecr.us-east-1.amazonaws.com/jenkins'
    registryCredential = 'jenkins-ecr'
    dockerimage = ''

     NEXUS_VERSION = "nexus3"
     NEXUS_PROTOCOL = "http"
     NEXUS_URL = "139.177.192.139:8081"
     NEXUS_REPOSITORY = "utrains-nexus-pipeline"
     NEXUS_CREDENTIAL_ID = "nexus-user-credentials"
     POM_VERSION = ''
}
    stages {

        // stage("build & SonarQube analysis") {  
        //     steps {
        //         echo 'build & SonarQube analysis...'
        //        withSonarQubeEnv('SonarServer') {
        //            sh 'mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=Hermann90_geo -X'
        //        }
        //     }
        // }
        // stage('Check Quality Gate') {
        //     steps {
        //         echo 'Checking quality gate...'
        //          script {
        //              timeout(time: 20, unit: 'MINUTES') {
        //                  def qg = waitForQualityGate()
        //                  if (qg.status != 'OK') {
        //                      error "Pipeline stopped because of quality gate status: ${qg.status}"
        //                  }
        //              }
        //          }
        //     }
        // }
        
         
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
                    jf "rt u target/${APP_NAME}-${POM_VERSION}.jar geolocation/${APP_NAME}-${POM_VERSION}.jar"
                    //sh "curl -uadmin:AP77hxSx85EFzMRQD9h9k5NQR1N -T target/${APP_NAME}-${POM_VERSION}.jar http://172.234.203.14:8081/artifactory/geolocation/${POM_VERSION}/${APP_NAME}-${POM_VERSION}.jar"
                    //dockerImage = docker.build registry + ":${POM_VERSION}"
                } 
            }
        }
        // stage('Deploy image') {
        //     steps{
        //         script{ 
        //             docker.withRegistry("https://"+registry,"ecr:us-east-1:"+registryCredential) {
        //                 dockerImage.push()
        //             }
        //         }
        //     }
        // } 

        // Project Helm Chart push as tgz file
        // stage("pushing the Backend helm charts to nexus"){
        //     steps{
        //         script{
        //             withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId:'nexus-pass', usernameVariable: 'jenkins-user', passwordVariable: 'docker_pass']]) {
        //                     def mavenPom = readMavenPom file: 'pom.xml'
        //                     POM_VERSION = "${mavenPom.version}"
        //                     sh "echo ${POM_VERSION}"
        //                     sh "tar -czvf  app-${POM_VERSION}.tgz app/"
        //                     sh "curl -u jenkins-user:$docker_pass http://139.177.192.139:8081/repository/geolocation/ --upload-file app-${POM_VERSION}.tgz -v"  
        //             }
        //         } 
        //     }
        // }     	    
    }
}