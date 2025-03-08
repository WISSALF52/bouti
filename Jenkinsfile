pipeline {
    agent any

    environment {
        MAVEN_HOME = '/opt/maven'  // Change this path to where Maven is installed on your Jenkins instance
        JAVA_HOME = '/opt/java/jdk-11' // Change this path to where JDK is installed
    }

    tools {
        // Configure the Maven and JDK installations in Jenkins Global Tool Configuration
        maven 'Maven 3'
        jdk 'OpenJDK 11'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from GitHub (assuming you are using GitHub)
                git 'https://github.com/yourusername/your-repository.git'
            }
        }

        stage('Compile') {
            steps {
                // Run Maven to compile the project
                script {
                    sh "'${MAVEN_HOME}/bin/mvn' clean compile"
                }
            }
        }

        stage('Test') {
            steps {
                // Run unit tests using Maven
                script {
                    sh "'${MAVEN_HOME}/bin/mvn' test"
                }
            }
        }

        stage('Package') {
            steps {
                // Create the packaged .jar file
                script {
                    sh "'${MAVEN_HOME}/bin/mvn' package"
                }
            }
        }

        stage('Deploy') {
            steps {
                // Deploy the application (for example, copy to a server or push to a container registry)
                // You can add your deployment steps here
                echo 'Deploying the application'
            }
        }
    }

    post {
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'There was a failure in the pipeline!'
        }
    }
}
