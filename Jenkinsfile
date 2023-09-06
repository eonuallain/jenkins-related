@NonCPS
def cancelPreviousBuilds() {
    def jobName = env.JOB_NAME
    def buildNumber = env.BUILD_NUMBER.toInteger()

    /* Get job name */
    def currentJob = Jenkins.instance.getItemByFullName(jobName)

    /* Iterating over the builds for specific job */
    for (def build : currentJob.builds) {
        def listener = build.getListener()
        def exec = build.getExecutor()
        /* If there is a build that is currently running and it's not current build */
        if (build.isBuilding() && build.number.toInteger() < buildNumber && exec != null) {
            /* Then stop it */
            exec.interrupt(
                    Result.ABORTED,
                    new CauseOfInterruption.UserInterruption("Aborted by #${currentBuild.getBuildCauses()[0].shortDescription}")
                )
            println("Aborted previously running build #${build.number}"
)        }
    }
}

node {
  stage('Clone sources') {
    git branch: 'main', url: 'https://github.com/eonuallain/jenkins-related.git'
  }


  stage('Cancel older builds') {
    echo "Checking for older running builds ..."
    cancelPreviousBuilds()
  }

  stage('Wait') {
    echo "waiting for 30 seconds ..."
    sleep 30
    echo "done waiting"
  }
}
