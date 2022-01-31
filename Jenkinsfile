/* groovylint-disable-next-line NglParseError */
pipeline {
    agent any 
        // docker {
        //     image 'maven:3-alpine'
        //     args '-v /root/.m2:/root/.m2'
        // }
    tools {
        maven 'maven'
        //jdk 'jdk-11'
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        // stage('Test') {
        //     steps {
        //         sh 'mvn test'
        //     }
        //     post {
        //         always {
        //             junit 'target/surefire-reports/*.xml'
        //         }
        //     }
        // }
        // stage('Deliver') {
        //     steps {
        //         sh './jenkins/scripts/deliver.sh'
        //     }
        // }
    }
    post {
        always {
            archiveArtifacts artifacts: '**/*.jar', fingerprint: true
        }
    }
        stage ('Upload to Google Storage') {
            steps {
                script {
                    gsutil cp '**/*.jar' gs://store_91
                }
            }
        }
}