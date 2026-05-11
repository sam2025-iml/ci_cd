pipeline {

    agent any

    // environment {
    //     FLUTTER_HOME = '/Users/bhaveshingeniousmindslab/fvm/default'
    //     PATH = "${FLUTTER_HOME}/bin:${env.PATH}"
    // }
     environment {
        PATH = "/usr/local/bin:${env.PATH}"
    }
    options {
        durabilityHint('PERFORMANCE_OPTIMIZED')
    }
    stages {

        stage('Docker check'){
            steps{
                sh 'which docker'
                sh 'docker --version'
            }
        }

//         stage('Flutter Version check') {
//             steps {
//                 sh 'flutter --version'
//             }
//         }

//         stage('Install Dependencies') {
//             steps {
//                 sh 'flutter pub get'
//             }
//         }

//         stage('Analyze') {
//             steps {
//                 sh 'flutter analyze'
//             }
//         }

//         stage('Build APK') {
//             steps {
//                 sh 'flutter build apk --release'
//             }
//         }
        
//         stage('Archive APK') {
//             steps {
//                  archiveArtifacts artifacts: 'build/app/outputs/flutter-apk/*.apk'
//             }
// }
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