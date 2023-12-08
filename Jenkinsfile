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
                sh "git config user.email odiadevops@gmail.com"
                sh "git config user.name devopsodia"
                sh "cat manifest/deployment.yaml"
                sh "sed -i 'vladoz77/cicd-test-project.*+1vladoz77/cicd-test-project:${TAG}+g' manifest/deployment.yaml"
                sh "cat manifest/deployment.yaml"
                sh "git add ."
                sh "git commit -m 'Done by Jenkins Job update manifest: ${TAG}'"
                
                withCredentials([string(credentialsId: 'githab-token', variable: 'github-pass')]) {
                    sh "git push https://github.com/vladoz77/gitops-test-project main"
                }
            }
        }
    }
  }
}

