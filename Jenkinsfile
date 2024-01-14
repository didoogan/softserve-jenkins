pipeline {
  agent {
    label 'remote-agent'  // Replace with your agent label
  }
  stages {
    stage('Install apache') {
      steps {
        sh 'sudo apt-get update'  // Assuming Debian-based OS
        sh 'sudo apt-get install -y apache2'
      }
    }

    stage('Check logs for errors') {
      steps {
        sh "echo 'Show error logs:'"
        sh "cat /var/log/apache2/*.log | grep 404"
      }
    }
  }
}
