pipeline {
    agent any

    environment {
        SONAR_PROJECT_KEY = 'my_organization:my_project:1.0'  // Replace with your actual project key
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
    }
}
