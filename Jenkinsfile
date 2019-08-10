pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('SonarQube analysis') {
            steps {
               script {
                   scannerHome = tool 'SonarQube Scanner 4.0'
               }
               withSonarQubeEnv('sonar'){
                   sh "${scannerHome}/bin/sonar-scanner -X"
               }
            }
        }
    }
}
