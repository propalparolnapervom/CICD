As secret is not shown in the Jenkins GUI by default, one way is to see it as saved artifact after job run

Example: Find out, what value of the `github-api-secret` secret
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
    
      // TO-DO: Insert AWS account (dev one in my case)
      image: <INSERT_AWS_ACC>.dkr.ecr.us-east-1.amazonaws.com/jenkins/jnlp
      command:
        - cat
      tty: true
"""
    }
  }
  stages {
    stage("Provision") {
      environment {
        CREDS = credentials('github-api-secret')
      }
      steps {
        sh "echo ${CREDS_USR} >> pw_foo"
        sh "echo ${CREDS_PSW} >> pw_foo"
        sh "cat pw_foo"
      }
      post { always { archiveArtifacts artifacts: "pw_foo" } }
    }
  }
}

```
