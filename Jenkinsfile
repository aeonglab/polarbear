def EUNHO

pipeline {
  agent any
  environment {
    DEVBUCKET="${BUCKET}"
    FLAG="FAIL"
    SPRING_PORT=""
  }
  stages {
    stage('ssh to comm and execute war') {
      steps {
        // sshagent(credentials: ['ubuntu']) {
        //   script {
        //     EUNHO = sh(script: '''
        //     ssh -o StrictHostKeyChecking=no -p ${PORT} ${TARGET_HOST}  '
        //     gcloud storage cp gs://ew1-dvs-dev-storage/communicator-$(date "+%Y-%m-%d").tar.gz /appl/communicator-$(date "+%Y-%m-%d").tar.gz
        //     tar -zxvf /appl/communicator-$(date "+%Y-%m-%d").tar.gz -C /appl/ > dev/null
        //     mv /appl/penguin-0.0.1-SNAPSHOT.war /appl/communicator-$(date "+%Y-%m-%d").war
        //     ./findport.sh > port.txt
        //     cat port.txt
        //     '
        //     ''', returnStdout:true).trim()
        //     echo "EUNHO: ${EUNHO}"
            
        //   }
        // }
        sshagent(credentials: ['ubuntu']) {
          script {
            EUNHO = sh(script: '''
            ssh -o StrictHostKeyChecking=no -p ${PORT} ${TARGET_HOST}  '
            FILENAME=communicator-$(date "+%Y-%m-%d")
            gcloud storage cp gs://ew1-dvs-dev-storage/$FILENAME.tar.gz /appl/$FILENAME.tar.gz
            tar -zxvf /appl/$FILENAME.tar.gz -C /appl/ > dev/null
            mv /appl/penguin-0.0.1-SNAPSHOT.war /appl/$FILENAME.war
            ./findport.sh > port.txt
            cat port.txt
            '
            ''', returnStdout:true).trim()
            echo "EUNHO: ${EUNHO}"
            
          }
        }
      }
    }
    // stage('http Request') {
    //   steps {
    //     script{
    //       echo "${EUNHO}"
    //       def RESPONSE_CODE = httpRequest "http://${target}:${EUNHO}"
    //       FLAG="${RESPONSE_CODE.status}"
    //       echo "${FLAG}"
    //     }
    //   }
    // }

    // stage('application success') {
    //   when {
    //     expression { "${FLAG}"=="200" }
    //   }
    //   steps {
    //     script {
    //       echo "success"
    //     }
    //   }
    // }
    
  }
}