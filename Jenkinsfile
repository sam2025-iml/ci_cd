pipeline {

    agent {
        docker {
            image 'ghcr.io/cirruslabs/flutter:stable'
            // tells Jenkins where to find docker on macOS
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    stages {

        stage('Flutter Version Check') {
            steps {
                sh 'flutter --version'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'flutter pub get'
            }
        }

        stage('Analyze') {
            steps {
                sh 'flutter analyze'
            }
        }

        stage('Build APK') {
            steps {
                sh 'flutter build apk --release'
            }
        }

        stage('Archive APK') {
            steps {
                archiveArtifacts artifacts: 'build/app/outputs/flutter-apk/*.apk'
            }
        }
    }

    post {
        success { echo '✅ Build Successful!' }
        failure  { echo '❌ Build Failed!' }
        always {
            script {
                if (currentBuild.rawBuild.getWorkspace() != null) {
                    cleanWs()
                }
            }
        }
    }
}