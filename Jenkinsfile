pipeline {
    agent any

    stages {
        stage('SCM') {
            steps {
                // Cloner le dépôt Git
                checkout scm
            }
        }

        stage('Compile') {
            steps {
                script {
                    // Utilisation de Maven pour compiler le projet
                    def mvn = tool name: 'Default Maven', type: 'Maven'
                    bat "\"${mvn}\\bin\\mvn\" clean compile"
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Lancer les tests unitaires avec Maven
                    def mvn = tool name: 'Default Maven', type: 'Maven'
                    bat "\"${mvn}\\bin\\mvn\" test"
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    // Lancer l'analyse SonarQube
                    def mvn = tool name: 'Default Maven', type: 'Maven'
                    withSonarQubeEnv() {
                        bat "\"${mvn}\\bin\\mvn\" clean verify sonar:sonar -Dsonar.projectKey=tique -Dsonar.projectName='tique'"
                    }
                }
            }
        }

        stage('Package') {
            steps {
                script {
                    // Emballer l'application en un fichier JAR (ou WAR, selon le projet)
                    def mvn = tool name: 'Default Maven', type: 'Maven'
                    bat "\"${mvn}\\bin\\mvn\" package"
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Déployer l'application (ajouter ici le script de déploiement selon ton besoin)
                    echo 'Déploiement en cours...'
                    // Exemple de déploiement (ajouter un script réel ici si nécessaire)
                }
            }
        }
    }

    post {
        always {
            // Actions à exécuter après la fin du pipeline (par exemple nettoyage)
            echo 'Pipeline terminé'
        }

        success {
            // Action en cas de succès du pipeline
            echo 'Le pipeline a réussi'
        }

        failure {
            // Action en cas d’échec du pipeline
            echo 'Le pipeline a échoué'
        }
    }
}
