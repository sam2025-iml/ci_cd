pipeline {

    agent any

    environment {
        FLUTTER_HOME = '/Users/bhaveshingeniousmindslab/fvm/default'
        PATH = "${FLUTTER_HOME}/bin:${env.PATH}"
    }

    stages {

        stage('Flutter Version check') {
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

        success {
            echo '✅ Build Successful!'
        }

        failure {
            echo '❌ Build Failed!'
        }

        always {
            cleanWs()
        }
    }
}