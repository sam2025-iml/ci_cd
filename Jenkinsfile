pipeline {

    agent {
        dockerfile {
            filename 'Dockerfile'
            additionalBuildArgs '--tag flutter-jenkins-builder:latest'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
            reuseNode true
        }
    }

    options {
        timestamps()
        timeout(time: 60, unit: 'MINUTES')
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }

    stages {

        stage('🔍 Verify Environment') {
            steps {
                sh 'flutter --version'
                sh 'java -version'
            }
        }

        stage('📦 Install Dependencies') {
            steps {
                sh 'flutter pub get'
            }
        }

        stage('🔎 Analyze') {
            steps {
                sh 'flutter analyze'
            }
        }

        stage('🧪 Test') {
            steps {
                sh 'flutter test'
            }
        }

        stage('🤖 Build Android APK') {
            steps {
                sh 'flutter build apk --release'
            }
        }
    }

    post {
        success {
            archiveArtifacts(
                artifacts: 'build/app/outputs/flutter-apk/*.apk',
                fingerprint: true
            )
            echo '✅ Build Successful! APK archived.'
        }
        failure {
            echo '❌ Build Failed! Check logs above.'
        }
        always {
            cleanWs(notFailBuild: true)
        }
    }
}