As secret is not shown in the Jenkins GUI by default, one way is to see it as saved artifact after job run

1. Create job (the one, where you inset job description as a script via Jenkins GUI);
2. Run it;
3. Go to the page with saved artifacts after job run.
4. Find the artifact with a secret and see it

```
pipeline {
  agent {
    kubernetes {
      yaml """
apiVersion: v1
kind: Pod
metadata:
  labels:
    name: cf-test-foo
  annotations:
    iam.amazonaws.com/role: jenkins-terraform
spec:
  containers:
    - name: jenkins
    
      // TO-DO: Insert AWS account (dev in my case)
      image: <INSERT_AWS_ACC>.dkr.ecr.us-east-1.amazonaws.com/jenkins/jnlp
      
      command:
        - cat
      tty: true
"""
    }
  }
  stages {
    stage("Provision") {
      steps {
        jobDsl scriptText: """
folder('temp/DataPlatform') {
    displayName('DataPlatform')
    description('Contains all the CI deployment and maintenance logic for GMC DataPlatform')
    properties {
      addExtensionNode {
      
        // TO-DO: Insert the GitHub name
        library(identifier: 'dataplatform_jenkins_libraries', retriever: modernSCM([$class: 'GitSCMSource', credentialsId: 'ds-github-ci', remote: 'https://github.com/<GITHUB_ACC_NAME>/dataplatform_jenkins_libraries.git', traits: [gitBranchDiscovery()]]))
      
      
      }
    }
}

pipelineJob('temp/foo') {
  definition {
    cpsScm {
      scriptPath('jenkins/deploy.jenkinsfile')
      scm {
        git {
          branch('dev')
          remote {
            name('origin')
            url('foo.git')
            credentials('ds-github-ci')
          }
        }
      }
    }
  }
}
"""
      }
    }
  }
}
```
