pipeline {
    agent { label 'kaniko'}

    stages {
        stage('Build and push to registry') {
            steps {
                container('kaniko') {
                    sh '''executor \
                          --destination=ssistla/myweb:1 \
                          --context=git://github.com/ssistla/playjenkins
                    '''
                }
            }
        }
    }
}
