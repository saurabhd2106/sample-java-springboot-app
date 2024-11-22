pipeline {

    agent {
        docker {
            image 'maven:3.9.9-eclipse-temurin-17'
        }
    }

    stages {
        stage("Verify Maven"){
            steps {
                sh 'mvn --version'
            }
        }

        stage("Clean"){
            steps {
                sh 'mvn clean'
            }
        }

        stage("Build, Test and Package"){
            steps {
                sh 'mvn package'
            }
        }
    }

    post {
        always {
            junit '**/target/surefire-reports/TEST-*.xml'
        }

        success {
            archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
        }
    }

}