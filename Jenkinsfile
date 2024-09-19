pipeline {
    agent any
    
    tools {
        maven 'MAVEN'
    }
    
    stages {
        stage ('Build & Unit Test') {
            steps {
                sh 'mvn clean verify -DskipITs=true'
                junit '**/target/surefire-reports/TEST-*.xml'
                archiveArtifacts 'target/*.jar'
            }
        }
        
        stage ('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('mylast') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
        
        stage ('Quality Gate') {
            steps {
                timeout(time: 1, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
