pipeline {
    agent {
        label 'maven'
    }
    
    tools {
        maven 'maven-3.9.11'
    }
    
    environment {
        SONAR_SCANNER = tool 'sonar-scanner'
    }
    
    stages {
        stage('Git Checkout') {
            steps {
                echo '<--------------- Cloning Repository --------------->'
                git branch: 'main', 
                    credentialsId: 'github-credentials',
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
        
        stage('SonarQube Analysis') {
            steps {
                echo '<--------------- SonarQube Analysis Started --------------->'
                withSonarQubeEnv('sonarcloud') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
        
        stage('Quality Gate') {
            steps {
                echo '<--------------- Quality Gate Check --------------->'
                timeout(time: 5, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
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
