pipeline {

  agent any 
  
  stages {
    
    stage('Build'){
      agent {
    kubernetes {
      label 'exmaple-kaniko-volume'
      yaml """
 apiVersion: v1
 kind: Pod
 metadata:
   name: kaniko
spec:
  containers:
  - name: kaniko
    image: gcr.io/kaniko-project/executor:debug
    args: ["--context=git://github.com/ssistla/playjenkins",
            "--destination=ssistla/justme/myweb:1"]
    volumeMounts:
      - name: kaniko-secret
        mountPath: /kaniko/.docker
  restartPolicy: Never
  volumes:
    - name: kaniko-secret
      secret:
        secretName: regcred
        items:
          - key: .dockerconfigjson
            path: config.json
"""            
    }
  }
    }

    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "mykubeconfig")
        }
      }
    }

  }
  }


