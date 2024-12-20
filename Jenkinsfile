@Library('mvnlibrary') _

pipeline {

    agent {
        docker {
            image 'maven:3.9.9-eclipse-temurin-17'
        }
    }

    stages {
        stage("Verify Maven"){
            steps {

                verifymvnversion()

                helloworld('world, Saurabh')

                script {

                    def message = sample.Helper.greet("Saurabh")

                    echo message
                }

                //sh 'mvn --version'
            }
        }

        stage("Clean"){
            steps {
                sh 'mvn clean'
            }
        }

        stage("Sonar Scan"){
            steps {
                withSonarQubeEnv('ec2-server') {
                    sh "mvn clean verify sonar:sonar -Dsonar.projectKey=sample-java-project -Dsonar.projectName='sample-java-project'"
                }
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