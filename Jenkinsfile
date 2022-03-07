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
                        <?xml version="1.0" ?>
<testsuites disabled="0" errors="0" failures="16" tests="924" time="0.0">
    <testsuite disabled="0" errors="0" failures="2" name="Ensure that load balancer is using TLS 1.2" package="checkov.terraform.checks.resource.aws.AppLoadBalancerTLS12" skipped="0" tests="14" time="0">
		<testcase classname="checkov.terraform.checks.resource.aws.AppLoadBalancerTLS12" file="/REDACTED/ec2/int_nlb.tf" name="terraform Ensure that load balancer is using TLS 1.2 aws_lb_listener.internal">
			<failure message="Resource &quot;aws_lb_listener.internal&quot; failed in check &quot;Ensure that load balancer is using TLS 1.2&quot;" type="failure"/>
		</testcase>
	</testsuite>
</testsuites>
EOF
                       '''
                }
            }
        }

        

    }
}

