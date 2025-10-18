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

        stage('Deploy to Tomcat') {
            steps {
                // Ensure 'Deploy to Container' plugin is installed in Jenkins
                // Ensure 'tomcat-credentials' is a Jenkins credential ID (Username with Password) for Tomcat manager
                // configured with a user having 'manager-script' role in Tomcat's tomcat-users.xml
                deploy adapters: [tomcat9(credentialsId: 'tomcat-credentials', url: 'http://18.61.69.33:8080')],
                        contextPath: 'webapp', // e.g., 'myapp'
                        war: 'target/*.war' // Adjust if your WAR file name differs
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