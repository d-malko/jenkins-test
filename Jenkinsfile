podTemplate(containers: [
  containerTemplate(
      name: 'groovy', 
      image: 'groovy:latest', 
      command: 'sleep', 
      args: '99d'
      )
  ], 
  
  volumes: [
  persistentVolumeClaim(
      mountPath: '/root/.m2/repository', 
      claimName: 'maven-repo-storage', 
      readOnly: false
      )
  ]) 

{
  node(POD_LABEL) {
    stage('Run shell script') {
//       git url: 'https://github.com/spring-projects/spring-petclinic.git', branch: 'main'
      container('groovy') {
        import java.util.concurrent.Callable
        import java.util.concurrent.Executors
        def sh(cmd) {
            def proc = ["/bin/sh", "-c", cmd].execute()
            def pool = Executors.newFixedThreadPool(2)
            def stdoutFuture = pool.submit({ -> proc.inputStream.text} as Callable<String>)
            def stderrFuture = pool.submit({ -> proc.errorStream.text} as Callable<String>)
            proc.waitFor()
            def exitValue = proc.exitValue()
            if(exitValue != 0) {
                System.err.println(stderrFuture.get())
                throw new RuntimeException("$cmd returned $exitValue")
            }
            return stdoutFuture.get()
        }
        def files = sh('ls $HOME').split()
      }
    }
  }
}
