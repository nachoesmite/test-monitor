#!groovy

env.DESIRED_NODE_NAME = env.DESIRED_NODE_NAME ?: 'docker'
env.GIT_CREDENTIALS_ID = env.GIT_CREDENTIALS_ID ?: 'github'
env.PIPELINE_ENV = env.PIPELINE_ENV ?: 'automation_qax'
env.MONITOR_ENVIRONMENT = 'qa'
env.MONITOR_URL = 'https://automation-builds.firebaseio.com'
    
    
    
def parameters = '''
environments {
    automation_qax {
        ENVS = 'qa'
    }
}
'''

node(env.DESIRED_NODE_NAME) {
    env.PROJECT_NAME = 'api-manager'
    env.PLATFORM = 'node'
    env.SKIP_STAGES = 'checkout,setup,unit-test,ui-test,junit-report,html-report,cobertura-report,slack-notification'

    
    stage "Basura"
    sh("exit 1")
    withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: env.GIT_CREDENTIALS_ID, passwordVariable: 'GITHUB_PASS', usernameVariable: 'GITHUB_USER']]) {
        git(credentialsId: env.GIT_CREDENTIALS_ID, url: 'git@github.com:mulesoft/automation-jenkins-pipeline.git', branch: 'post-to-dashboard')
        load('pipeline.groovy').execute(parameters, env.PIPELINE_ENV)
    }
}
