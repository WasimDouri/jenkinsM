pipeline {
    agent any
    // Add a tool configuration here...
    stages {
        stage('Source') {
            steps {
                git branch: 'main',
                    changelog: false,
                    poll: false,
                    url: 'https://github.com/WasimDouri/jenkinsM.git'
            }
        }
        stage('Clean') {
            steps {
                dir("${env.WORKSPACE}/src"){
                    echo "Cleaning the workspace..."
                    // Uncomment the following line after Maven is configured as a global tool
                     sh 'mvn clean'
                }
            }
        }
        stage('Test') {
            steps {
                dir("${env.WORKSPACE}/src"){
                    echo "Running tests..."
                    // Uncomment the following line after Maven is configured as a global tool
                     sh 'mvn test'
                }
            }
        }
        stage('Package') {
            steps {
                dir("${env.WORKSPACE}/src"){
                    echo "Creating the JAR file..."
                    // Uncomment the following line after Maven is configured as a global tool
                     sh 'mvn package -DskipTests'
                }
            }
        }
    }
    post {
        always {
            junit allowEmptyResults: true,
                testResults: '**/TEST-com.jenkinsM.AppTest.xml'

            archiveArtifacts allowEmptyArchive: true,
                artifacts: '**/hello-1.0-SNAPSHOT.jar'
        }
    }
}
