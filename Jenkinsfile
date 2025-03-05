// Jenkins Pipeline Script 
pipeline {
    agent any

    environment {
        ARDUINO_CLI = "C:\\arduino-cli\\arduino-cli.exe"  // Update with actual path
        SKETCH_NAME = "Blink"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/pujaperumal/arduino-ci-cd.git'
            }
        }

        stage('Validate Sketch') {
            steps {
                script {
                    bat "${ARDUINO_CLI} sketch new ${SKETCH_NAME}"
                }
            }
        }

        stage('Compile Sketch') {
            steps {
                script {
                    bat "${ARDUINO_CLI} compile --fqbn arduino:avr:uno ${SKETCH_NAME}"
                }
            }
        }
    }

    post {
        success {
            echo 'Compilation successful!'
        }
        failure {
            echo 'Compilation failed. Check logs for errors.'
        }
    }
}
