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
        stage("Docker"){
            steps{
                sh'''
                cd FlightReservationApplication
                docker build -t abhinav2912/flight-reservation:latest .
                docker push abhinav2912/flight-reservation:latest
                '''
            }
        }
        stage("k8's"){
            steps{
                sh'''
                cd FlightReservationApplication
                 kubectl apply -f k8s/deployment.yaml
                kubectl apply -f k8s/service.yaml
                '''
            }
        }
    }
}
