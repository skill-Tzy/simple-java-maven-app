node {
    docker.image('maven:3.9.6-eclipse-temurin-17-alpine').inside('-v /root/.m2:/root/.m2') {
        try {
            stage('Build') {
                sh 'mvn -B -DskipTests clean package'
            }

            stage('Test') {
                sh 'mvn test'
                junit 'target/surefire-reports/*.xml'
            }

            stage('Deliver') {
                sh './jenkins/scripts/deliver.sh'
            }

        } catch (Exception e) {
            currentBuild.result = 'FAILURE'
            throw e
        } finally {
            // You can add any cleanup steps here
        }
    }
}
