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
            sh "echo build number is $TAG"
        }
    }
  }
}

