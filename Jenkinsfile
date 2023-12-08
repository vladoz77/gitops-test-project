pipeline{
  agent "any"
  environment{
    TAG = "1.2.3"
  }
  stages{
    stage("Clean-workspace"){
        steps{
            cleanWs()
        }
    }
    stage("checkout from scm"){
        steps{
          git branch: 'main', url: 'https://github.com/vladoz77/gitops-test-project'
        }
    }

    stage("test variables"){
        steps{
            script{
                sh "git config user.email vladoz77@yandex.com"
                sh "git config user.name vlado77"
                sh "cat manifest/deployment.yaml"
                sh "sed -i 's+vladoz77/cicd-test-project.*+vladoz77/cicd-test-project:${TAG}+g' manifest/deployment.yaml"
                sh "cat manifest/deployment.yaml"
                sh "git add ."
                sh "git commit -m 'Done by Jenkins Job update manifest: ${TAG}'"
                
                withCredentials([gitUsernamePassword(credentialsId: 'github', gitToolName: 'Default')]) {
                    sh "git push https://github.com/vladoz77/gitops-test-project main"
                }
            }
        }
    }
  }
}

