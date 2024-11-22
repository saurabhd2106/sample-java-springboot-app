pipeline {

    angent {
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
    }

}