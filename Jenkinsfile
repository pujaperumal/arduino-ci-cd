pipeline {
    agent any

    environment {
        ARDUINO_CLI = 'arduino-cli' // Assuming it's in the system PATH
        BOARD_FQBN = 'arduino:avr:uno' // Set the board type
        SKETCH_NAME = 'Blink.ino' // Change to match your file
        GIT_REPO = 'https://github.com/pujaperumal/arduino-ci-cd.git' // Your GitHub repo
        GIT_BRANCH = 'main' // Change branch if needed
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
                    bat "${ARDUINO_CLI} compile --fqbn ${BOARD_FQBN} --warnings all ${SKETCH_NAME}"
                }
            }
        }

        stage('Compile Sketch') {
            steps {
                script {
                    echo 'Compiling the Arduino sketch...'
                    bat "${ARDUINO_CLI} compile --fqbn ${BOARD_FQBN} ${SKETCH_NAME}"
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
