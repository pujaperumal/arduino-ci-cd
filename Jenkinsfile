pipeline {
    agent any

    stages {
        // Stage 1: Clone the repository
        stage('Clone Repository') {
            steps {
                checkout scm // Dynamically checks out the repository configured in the Jenkins job
            }
        }

        // Stage 2: Install Arduino CLI (if not already installed)
        stage('Install Arduino CLI') {
            steps {
                script {
                    // Check if Arduino CLI is already installed
                    def arduinoCliInstalled = bat(script: 'where arduino-cli', returnStatus: true) == 0
                    if (!arduinoCliInstalled) {
                        // Download and install Arduino CLI
                        bat 'curl -fsSL https://raw.githubusercontent.com/arduino/arduino-cli/master/install.sh -o install.sh'
                        bat 'bash install.sh'
                    } else {
                        echo 'Arduino CLI is already installed.'
                    }

                    // Set up Arduino CLI (install board packages)
                    bat 'arduino-cli core install arduino:avr'
                }
            }
        }

        // Stage 3: Compile the Arduino sketch
        stage('Compile Sketch') {
            steps {
                script {
                    // Compile the sketch for Arduino Uno
                    def sketchFile = 'Arduino-CI.ino' // Replace with your actual sketch file name
                    def compileResult = bat(script: "arduino-cli compile --fqbn arduino:avr:uno ${sketchFile}", returnStatus: true)
                    
                    // Fail the pipeline if compilation fails
                    if (compileResult != 0) {
                        error 'Sketch compilation failed!'
                    } else {
                        echo 'Sketch compiled successfully!'
                    }
                }
            }
        }
    }

    // Post-build actions
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the logs for details.'
        }
    }
}
