pipeline {
  agent any

  stages {
    stage('Check Apache Logs') {
      steps {
        script {
          sh """
            #!/bin/bash

            log_file="/var/log/apache2/error.log"
            has_errors=false

            while IFS= read -r line; do
              if [[ \$line =~ [45][0-9][0-9] ]]; then
                has_errors=true
                break
              fi
            done < "\$log_file"

            if [[ \$has_errors = false ]]; then
              echo "There are no 4** or 5** errors in the log file."
            else
              echo "There are some 4** or 5** errors in the log file."
            fi
          """
        }
      }
    }
  }
}
