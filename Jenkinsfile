pipeline {
  agent any
  environment {
    APPSYSID = '3d8b478c2f60b0102d3b49e72799b65f'
    BRANCH = "${BRANCH_NAME}"
    CREDENTIALS = 'ServiceNow'
    DEVENV = 'https://dev57819.service-now.com/'
    PRODENV = 'https://dev108915.service-now.com/'
   
  }
  stages {
    stage('Build') {
      when {
        not {
          branch 'master'
        }
      }
      steps {
        snApplyChanges(appSysId: "${APPSYSID}", branchName: "${BRANCH}", url: "${DEVENV}", credentialsId: "${CREDENTIALS}")
        snPublishApp(credentialsId: "${CREDENTIALS}", appSysId: "${APPSYSID}", obtainVersionAutomatically: true, url: "${DEVENV}")
      }
    }
 
    stage('Deploy to Prod') {
      when {
        branch 'master'
      }
      steps {
        snInstallApp(credentialsId: "${CREDENTIALS}", url: "${PRODENV}", appSysId: "${APPSYSID}")
      }
    }
  }
}
