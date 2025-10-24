pipeline {
    agent any

    options {
        // If any stage becomes unstable, skip the rest
        skipStagesAfterUnstable()
    }

    tools {
        // Use the Maven tool configured in Jenkins (Manage Jenkins → Global Tool Configuration)
        maven '3.9.11'
    }

    stages {

        stage('Checkout Source Code') {
            steps {
                // Replace with your own GitHub repo URL
                git branch: 'main', url: 'https://github.com/yourusername/your-springboot-repo.git'
            }
        }

        stage('Test') {
            steps {
                // Verify Git and Maven are available, then run tests
                sh 'git --version'
                sh 'mvn --version'
                sh 'mvn clean test'
            }
        }

        stage('Build and Package') {
            steps {
                // Build the fat JAR, skipping tests since they already ran above
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Archive Artifacts') {
            steps {
                // Save the generated JAR so Jenkins can store it as a build artifact
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Build successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}

