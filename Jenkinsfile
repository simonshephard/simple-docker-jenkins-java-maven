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
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh 'id'
                sh 'whoami'
                sh 'cp ./jenkins/scripts/deliver.sh ./jenkins/scripts/deliver_copy.sh'
                sh 'chmod 777 ./jenkins/scripts/deliver_copy.sh'
                sh './jenkins/scripts/deliver_copy.sh'
            }
        }
    }
}
