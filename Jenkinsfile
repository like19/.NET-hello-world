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

        stage ('Upload to google bucker') {
            steps {
                googleStorageUpload bucket: 'gs://store_91', credentialsId: 'floow-clusters', pattern: '**/*.jar'
            }
        }

    }
    post {
        always {
            archiveArtifacts artifacts: '**/*.jar', fingerprint: true
        }
    }
}