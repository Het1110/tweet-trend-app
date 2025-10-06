pipeline {
    agent {
        label 'maven'
    }
    
    tools {
        maven 'maven-3.9.5'
    }
    
    stages {
        stage('Git Checkout') {
            steps {
                echo '<--------------- Cloning Repository --------------->'
                git branch: 'main', 
                    url: 'https://github.com/Het1110/tweet-trend-app.git'
            }
        }
        
        stage('Build') {
            steps {
                echo '<--------------- Building Application --------------->'
                sh 'mvn clean install -DskipTests'
            }
        }
        
        stage('Test') {
            steps {
                echo '<--------------- Running Tests --------------->'
                sh 'mvn test'
            }
        }
    }
    
    post {
        always {
            echo 'Pipeline execution completed'
        }
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline execution failed!'
        }
    }
}
