pipeline {
    agent any  // Spécifie un agent générique

    stages {
        stage('Checkout') {
            steps {
                // Récupère le code depuis GitHub
                git 'https://github.com/WISSALF52/boutique.git'
            }
        }

        stage('Compile') {
            steps {
                // Compile le projet avec Maven
                script {
                    sh 'mvn clean compile'
                }
            }
        }

        stage('Test') {
            steps {
                // Lance les tests unitaires avec Maven
                script {
                    sh 'mvn test'
                }
            }
        }

        stage('Package') {
            steps {
                // Crée le fichier .jar avec Maven
                script {
                    sh 'mvn package'
                }
            }
        }

        stage('Deploy') {
            steps {
                // Déploie l'application (exemple de message ici, à personnaliser selon ton processus de déploiement)
                echo 'Déploiement de l\'application'
            }
        }
    }

    post {
        success {
            echo 'Construction et déploiement réussis !'
        }
        failure {
            echo 'Échec de la pipeline !'
        }
    }
}
