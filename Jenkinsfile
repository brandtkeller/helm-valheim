pipeline {
    agent none
 
   environment {
         GITHUB_REPO = 'github.com/brandtkeller/helm-valheim.git'
    }
    options {
        skipStagesAfterUnstable()
        skipDefaultCheckout false
    }
    stages {
        stage('Build Stages') {
            agent { label 'jenkins-base-agent' }
            stages {
                stage('Feature Branch') {
                    when { not { branch 'master' } }
                    steps {
                        sh 'helm lint'
                    }
                }
                stage('Master Branch') {
                    when { branch 'master' }
                    steps {
                        sh 'helm lint'
                        sh 'echo "package and push the chart to some remote helm registry"'
                    }
                }
                stage('Mirror to public Github') {
                    when { branch 'master' }
                        steps {
                            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                            withCredentials([usernamePassword(credentialsId: 'git_token', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                                    sh 'git fetch --prune'
                                    sh 'git push --prune https://$GIT_USERNAME:$GIT_PASSWORD@$GITHUB_REPO +refs/remotes/origin/*:refs/heads/* +refs/tags/*:refs/tags/*'
                                }
                            }
                        }

                }
            }
        }
    }
}