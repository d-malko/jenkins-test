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
                        cat >  new.log <<EOF
                        <<testsuite tests="3">
			    <testcase classname="foo1" name="ASuccessfulTest"/>
			    <testcase classname="foo2" name="AnotherSuccessfulTest"/>
			    <testcase classname="foo3" name="AFailingTest">
				<failure type="NotEnoughFoo"> details about failure </failure>
			    </testcase>
			</testsuite>

			EOF
                       '''
		script{
			junit "new.log"
		}
                }
            }
        }

        

    }
}

