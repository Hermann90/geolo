pipeline {
    agent any

    environment {
        // Define environment variables
        GIT_REPO = 'https://github.com/Hermann90/geolo.git'
        SONAR_HOST_URL = 'http://54.177.126.245:9000'
        ARTIFACTORY_URL = 'http://54.177.126.245:8082'
        ARTIFACTORY_REPO = 'your-repo-name'

        // AWS_REGION = 'us-east-1'
        // SCANNER_HOME= tool 'sonar'
        // ARTIFACTORY_URL=  'http://54.177.126.245:8082/artifactory'
        // REPO = 'geolocation'
        // APP_NAME = 'geoapp'
        // APP_OWNER = 'cloud_team'
        // DOCKER_REPO_NAME = "${APP_NAME}"
        // REPO_URL     = 'public.ecr.aws/g0j7o9l5'
        // DOCKER_REPO = "${REPO_URL}/${DOCKER_REPO_NAME}"
        // BRANCH_NAME= 'main'
        // GIT_CRED = 'GITHUB_CRED'
        // KUBERNETES_CRED = 'KUBERNETES_CRED'
        // KUBERNETES_URL = 'https://104.237.133.213:6443'
        // SONAQUBE_CRED = 'sonarqube_ID'
        // SONAQUBE_INSTALLATION = 'Sonarqube'
        // JFROG_CRED = 'j_frog-cred'
        // PROJECT_URL = 'https://github.com/Hermann90/geolo.git'
        // ARTIFACTPATH = 'target/*.jar'
        // ARTIFACTTARGETPATH = "release_${BUILD_ID}.jar"
        // HELMARTIFACTPATH = "geoapp-${BUILD_ID}.tgz"
        // HELMARTIFACTTARGET = "heml/geoapp-${BUILD_ID}.tgz"
    }

    stages {
        stage('Checkout') {
            steps {
                // Pull code from Git
                git branch: 'main', url: env.GIT_REPO
            }
        }

        stage('Unit Test'){
            steps{
                sh 'mvn clean'
                sh 'mvn compile '
                sh 'mvn test'
            }
        }

        // stage('Fetch Secrets from Vault') {
        //     steps {
        //         // Fetch SonarQube token from Vault
        //         withVaultSecrets(secrets: [
        //             [path: 'secret/jenkins/sonarqube', engineVersion: 2, secretValues: [
        //                 [vaultKey: 'auth_token', envVar: 'SONAR_AUTH_TOKEN']
        //             ]],
        //             [path: 'secret/jenkins/artifactory', engineVersion: 2, secretValues: [
        //                 [vaultKey: 'username', envVar: 'ARTIFACTORY_USERNAME'],
        //                 [vaultKey: 'password', envVar: 'ARTIFACTORY_PASSWORD']
        //             ]]
        //         ]) {
        //             echo 'Secrets fetched from Vault successfully!'
        //         }
        //     }
        // }

        // stage('Build') {
        //     steps {
        //         // Build the project using Maven
        //         sh 'mvn clean install'
        //     }
        // }

        // stage('Unit Tests') {
        //     steps {
        //         // Run unit tests
        //         sh 'mvn test'
        //     }
        // }

        // stage('SonarQube Analysis') {
        //     steps {
        //         // Run SonarQube analysis using the token fetched from Vault
        //         withSonarQubeEnv('sonar-server') {
        //             sh "mvn sonar:sonar -Dsonar.projectKey=your-project-key -Dsonar.login=${env.SONAR_AUTH_TOKEN}"
        //         }
        //     }
        // }

        // stage('Publish to Artifactory') {
        //     steps {
        //         // Publish the build artifact to JFrog Artifactory using credentials fetched from Vault
        //         rtUpload (
        //             serverId: 'artifactory-server',
        //             spec: '''{
        //                 "files": [
        //                     {
        //                         "pattern": "target/*.jar",
        //                         "target": "${ARTIFACTORY_REPO}/your-project-path/"
        //                     }
        //                 ]
        //             }''',
        //             username: env.ARTIFACTORY_USERNAME,
        //             password: env.ARTIFACTORY_PASSWORD
        //         )
        //     }
        // }

        // stage('Deploy') {
        //     steps {
        //         // Deploy the artifact to a target environment
        //         sh 'echo "Deploying artifact to target environment..."'
        //         // Add deployment logic here (e.g., SSH, Kubernetes, etc.)
        //     }
        // }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}