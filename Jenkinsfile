properties([
  parameters([
    choice(
      name: 'ENVIRONMENT',
      choices: ['dev', 'test', 'devops', 'staging', 'prod']
    ),
  ])
])

if("staging"=="${ENVIRONMENT}") {
  stage('Deploy approval'){
    input "Deploy to ${ENVIRONMENT}? Branch name: ${env.BRANCH_NAME}"
  }
}

node {
  try {
    deleteDir()
    checkout scm
    echo "HELLO WORLD!!!"
       def props = readProperties file: "${ENVIRONMENT}-config.properties"
       def skip_tests = props['skip_tests']
       if (skip_tests == 'true') {
          print 'skipping tests'
       } else {
          print 'running tests'
       }
       if('staging' != "${ENVIRONMENT}" && 'prod' != "${ENVIRONMENT}") {
        print 'Development'
       }
       if('staging' == "${ENVIRONMENT}" || 'prod' == "${ENVIRONMENT}") {
        print 'Production'
       }
  }
  finally {
    deleteDir()
  }
}
