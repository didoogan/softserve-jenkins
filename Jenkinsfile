pipeline {
    agent any  
    stages {
        stage('Install apache') {
            steps {
                sh 'sudo apt-get update'  // Assuming Debian-based OS
                sh 'sudo apt-get install -y apache2'
            }
        }

        stage('Check logs for errors') {
            steps {
                script {
                    def logFile = '/var/log/apache2/error.log'  // Adjust path if needed
                    def errors = readFile(logFile)
                                      .split('\n')
                                      .findAll { it =~ /(4|5)\d\d/ }

                    if (!errors.isEmpty()) {
                        echo "Errors found in ${logFile}:"
                        errors.each { echo "- ${it}" }
                        currentBuild.result = 'UNSTABLE'  // Mark build as unstable
                    } else {
                        echo "No 4xx or 5xx errors found in ${logFile}"
                    }
                }
            }
        }
    }
}
