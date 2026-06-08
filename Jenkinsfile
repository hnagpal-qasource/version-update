pipeline {
     parameters {
        // Creates a dropdown menu for selection
        choice(
            name: 'AGENT_IMAGE', 
            choices: ['node:20-alpine', 'node:18-alpine', 'maven:3.9-eclipse-temurin-17', 'python:3.11-alpine'], 
            description: 'Select the container image to run this pipeline agent'
        )
        // Alternative: Creates a free-text input box if you want to type any image manually
        // string(name: 'CUSTOM_IMAGE', defaultValue: 'node:20-alpine', description: 'Type any custom image')
    }
    agent {
        docker {
            // The container image you want your code to run inside
              image "${params.AGENT_IMAGE}"
            // Optional: Reuses the same workspace directory structure on the host
            reuseNode true 
        }
    }

    stages {
        stage('Verify Environment') {
            steps {
                // These commands execute safely inside your isolated node container
                echo 'Checking software versions inside the container...'
                sh 'node -v'
                sh 'npm -v'
            }
        }
        stage('Application Build') {
            steps {
                echo 'Building code inside the isolated container...'
                // sh 'npm install && npm run build'
            }
        }
    }
}
