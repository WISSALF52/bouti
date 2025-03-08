pipeline {
    agent any  // Spécifie un agent générique

    stages {
        stage('Checkout') {
            steps {
                // Récupère le code depuis GitHub
                git 'https://github.com/WISSALF52/bouti.git'
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

        stage('SonarQube Analysis') {
            steps {
                // Effectue l'analyse SonarQube
                script {
                    def mvn = tool 'maven'
                    withSonarQubeEnv() {
                     bat "\"C:\\Program Files\\apache-maven-3.9.9\\bin\\mvn\" clean verify sonar:sonar -Dsonar.projectKey=anf -Dsonar.projectName=anf"

                    }
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
