pipeline {
    agent any

    stages {
        

        stage('Nettoyage et Compilation avec Maven') {
            steps {
                // Nettoyage du projet avec Maven
                sh 'mvn clean'
                
                // Compilation du projet avec Maven
                sh 'mvn compile'
            }
        }
    }
}
