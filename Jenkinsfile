pipeline {
    agent any // Specifies that the pipeline can run on any available agent

    tools {
        // Defines the Maven and JDK installations to be used.
        // These names should match the configurations in Manage Jenkins > Global Tool Configuration.
        maven 'Maven 3.9.11' 
        // jdk 'JDK 21' 
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', credentialsId: 'github_credentials', url: 'https://github.com/saikrishnakolakanda/webapp.git'
                // Replace 'main' with your target branch, 'your-github-credentials-id' with your Jenkins credentials ID for GitHub,
                // and 'https://github.com/your-username/your-repository.git' with your repository URL.
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package' // Executes the Maven build command
            }
        }
    }

    post {
        always {
            // Actions to perform regardless of the build result
            echo 'Pipeline finished.'
        }
        success {
            // Actions to perform on successful build
            echo 'Build successful!'
        }
        failure {
            // Actions to perform on failed build
            echo 'Build failed!'
        }
    }
}