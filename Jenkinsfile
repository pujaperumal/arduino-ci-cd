pipeline {
    agent any
    environment {
        ARDUINO_CLI = "C:\\Users\\P PUJA\\Downloads\\arduino-cli_1.2.0_Windows_64bit\\arduino-cli.exe"
    }
    stages {
        stage('Validate Sketch') {
            steps {
                script {
                    bat '"C:\\Windows\\System32\\cmd.exe" /c "%ARDUINO_CLI% compile --fqbn arduino:avr:uno Blink.ino"'
                }
            }
        }
        stage('Compile Sketch') {
            steps {
                script {
                    bat '"C:\\Windows\\System32\\cmd.exe" /c "%ARDUINO_CLI% compile --fqbn arduino:avr:uno Blink.ino"'
                }
            }
        }
    }
    post {
        failure {
            echo 'Compilation failed. Check logs for errors.'
        }
    }
}
