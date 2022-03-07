podTemplate(containers: [
    containerTemplate(
        name: 'groovy', 
        image: 'groovy:latest', 
        command: 'sleep', 
        args: '30d')
  ]) {

    node(POD_LABEL) {
        stage('build') {
            container('groovy') {
                stage('Build a Maven project') {
                    sh '''
                    echo "groovy build"
                    '''
                }
            }
        }

        

    }
}

