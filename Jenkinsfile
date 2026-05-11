pipeline {

    agent any

    environment {
        PATH = "/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:${env.PATH}"
    }

    options {
        timestamps()
        timeout(time: 60, unit: 'MINUTES')
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }

    stages {

        stage('🔍 Checkout') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('⚙️ Flutter Version') {
            steps {
                sh 'flutter --version'
                sh 'flutter doctor'
            }
        }

        stage('📦 Install Dependencies') {
            steps {
                sh 'flutter pub get'
            }
        }

        stage('🔎 Analyze Code') {
            steps {
                sh 'flutter analyze'
            }
        }

        stage('🧪 Run Tests') {
            steps {
                sh 'flutter test'
            }
        }

        stage('🤖 Build Android APK') {
            steps {
                sh 'flutter build apk --release'
            }
            post {
                success {
                    archiveArtifacts(
                        artifacts: 'build/app/outputs/flutter-apk/*.apk',
                        fingerprint: true
                    )
                }
            }
        }

        stage('🍎 Build iOS') {
            steps {
                sh 'flutter build ios --release --no-codesign'
            }
            post {
                success {
                    archiveArtifacts(
                        artifacts: 'build/ios/iphoneos/*.app',
                        fingerprint: true
                    )
                }
            }
        }
    }

    post {
        success {
            echo '✅ Build Successful! APK and iOS app are archived.'
        }
        failure {
            echo '❌ Build Failed! Check the logs above.'
        }
        always {
            cleanWs(notFailBuild: true)
        }
    }
}