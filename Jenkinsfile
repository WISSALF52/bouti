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
