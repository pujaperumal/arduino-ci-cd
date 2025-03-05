pipeline {
    agent any

    environment {
        ARDUINO_CLI = 'C:\\Users\\P PUJA\\Downloads\\arduino-cli_1.2.0_Windows_64bit\\arduino-cli.exe' 
        BOARD_FQBN = 'arduino:avr:uno'
        SKETCH_NAME = 'Blink.ino'
        GIT_REPO = 'https://github.com/pujaperumal/arduino-ci-cd.git'
        GIT_BRANCH = 'main'
    }

    stages {
        stage('Checkout Code') {
            steps {
                script {
                    echo 'Checking out latest code from GitHub...'
                    git branch: "${GIT_BRANCH}", url: "${GIT_REPO}"
                }
            }
        }

        stage('Validate Sketch') {
            steps {
                script {
                    echo 'Validating Arduino sketch syntax...'
                    bat "cmd.exe /c \"${ARDUINO_CLI} compile --fqbn ${BOARD_FQBN} --warnings all ${SKETCH_NAME}\""
                }
            }
        }

        stage('Compile Sketch') {
            steps {
                script {
                    echo 'Compiling the Arduino sketch...'
                    bat "cmd.exe /c \"${ARDUINO_CLI} compile --fqbn ${BOARD_FQBN} ${SKETCH_NAME}\""
                }
            }
        }
    }

    post {
        success {
            echo '✅ Build succeeded! Arduino sketch compiled successfully.'
        }
        failure {
            echo '❌ Build failed! Check the logs for errors.'
        }
    }
}
