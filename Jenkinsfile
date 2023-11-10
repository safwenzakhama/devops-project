pipeline {
    agent any

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
                     withSonarQubeEnv('sq1') {
                    sh 'SonarQubeScanner/bin/sonar-scanner'
                }
                }
            }
        }
    }
}
