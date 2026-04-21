pipeline {
    agent any

    stages {

        stage('Pull') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/mayurmwagh/flight-reservation-app.git'
            }
        }

        stage('Build') {
            steps {
                dir('FlightReservationApplication') {
                    sh 'JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64 mvn clean package -DskipTests'
                }
            }
        }
        stage('SonarQube Analysis') {
            steps {
                dir('FlightReservationApplication') {
                    withSonarQubeEnv('SonarQube') {
                        sh 'JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64 mvn sonar:sonar'
                    }
                }
            }
    }
    }
}
