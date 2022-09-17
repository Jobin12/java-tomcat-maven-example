pipeline{
    agent any
    stages{
        stage('SCM Checkout'){
            steps{
                git 'https://github.com/Jobin12/java-tomcat-maven-example.git'
            }
        }
        stage('sonarqube analysis') {
            environment {
                SCANNER_HOME = tool 'SonarQube'
                PROJECT_NAME = "Java-maven2"
            }
            steps {
                script {
                    withSonarQubeEnv('SonarQube') {
                        sh '''$SCANNER_HOME -Dsonar.projectKey=$PROJECT_NAME \
                        -Dsonar.java.binaries=\"target/classes/\"'''
                    }
                }
            }
        }
        stage('Build'){
            steps{
                sh 'mvn package'
            }
        }
        stage('Deploy'){
            steps{
                sh 'sudo cp /var/lib/jenkins/workspace/maven-test/target/java-tomcat-maven-example.war /opt/apache-tomcat-9.0.65/webapps'
            }
        }
        stage('Post Build'){
            steps{
                sh 'echo "Build Successful"'
            }
        }
    }
}
