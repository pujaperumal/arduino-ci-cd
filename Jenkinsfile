pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/pujaperumal/Arduino-CI.git'
            }
        }

        stage('Install Arduino CLI') {
            steps {
                sh 'curl -fsSL https://raw.githubusercontent.com/arduino/arduino-cli/master/install.sh | sh'
            }
        }

        stage('Compile Sketch') {
            steps {
                sh 'arduino-cli compile --fqbn arduino:avr:uno Arduino-CI.ino'
            }
        }

        
    }
}
