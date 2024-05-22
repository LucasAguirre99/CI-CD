pipeline {
    agent any

    triggers {
        githubPush()
    }


    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the repository
                checkout scm
            }
        }
        
        stage('Validate Python File') {
            steps {
                script {
                    def pyFiles = findFiles(glob: '**/*.py')
                    if (pyFiles.size() > 0) {
                        pyFiles.each { file ->
                            echo "Validating ${file}"
                            sh "python -m py_compile ${file}"
                        }
                    } else {
                        echo "No .py files found to validate"
                    }
                }
            }
        }
    }

    post {
        failure {
            echo "Python file validation failed."
            // Optionally, send a notification
        }
        success {
            echo "Python file validation succeeded."
            // Optionally, perform additional actions
        }
    }
}

