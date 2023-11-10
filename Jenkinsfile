pipeline {
    agent any

    environment {
        SONAR_PROJECT_KEY = 'Devops:Backend:1.0'  // Replace with your actual project key
        SNAP_REPO = 'vprofile-snapshot'
        NEXUS_USER = 'admin'
        NEXUS_PASS = 'nexus'
        RELEASE_REPO = 'vprofile-release'
        CENTRAL_REPO = 'vpro-maven-central'
        NEXUSIP = '192.168.33.10'
        NEXUSPORT = '8081'
        NEXUS_GRP_REPO = 'vpro-maven-group'
        NEXUS_LOGIN = 'nexuslogin'
        NEXUSPASS = credentials('nexuspass')
    }

    stages {
        stage('Clean and Build with Maven') {
            steps {
                // Nettoyage du projet avec Maven
                sh 'mvn clean'
                
                // Compilation du projet avec Maven
                sh 'mvn compile'
            }
        }

        stage('Tests et SonarQube Analysis') {
            steps {
                // Exécution des tests avec Maven
                sh 'mvn test'

                // Lancement de l'analyse SonarQube
                script {
                    def scannerHome = tool 'SonarQubeScanner'
                    withSonarQubeEnv('sq1') {
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=${SONAR_PROJECT_KEY} -Dsonar.java.binaries=target/classes"
                    }
                }
            }
        }

        stage('Deploy to Nexus') {
            steps {
                script {
                    // Deploy Maven artifacts to Nexus releases or snapshots based on the version
                    if (env.BUILD_IS_SNAPSHOT == 'true') {
                        sh "mvn deploy -DrepositoryId=${NEXUS_SNAPSHOTS_ID} -Durl=${NEXUS_URL}"
                    } else {
                        sh "mvn deploy -DrepositoryId=${NEXUS_RELEASES_ID} -Durl=${NEXUS_URL}"
                    }
                }
            }
        }
    }
}
