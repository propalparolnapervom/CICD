# Groovy Scripts examples

So Jenkins has a window to run Groovy scripts (somewhere here https://jenkins.datasenate.io/computer/(master)/script)

`Dashboard` -> `Manage Jenkins` -> `Manage Nodes and Clouds` -> Click on node (probably, `master`) -> `Script Console`

## How to kill zombie job
`JobFullPath` is the `Full project name` you can find on the web-page of the branch for your Job.

```
def zombieJobFullPath = 'Full/Job/Path'
def zombieJobBuildId = 1
Jenkins.instance.getItemByFullName(zombieJobFullPath)
                .getBuildByNumber(zombieJobBuildId)
                .finish(
                        hudson.model.Result.ABORTED,
                        new java.io.IOException("Aborting build")
                )

```

## How to purge the Jenkins Build Queue
```
def q = Jenkins.instance.queue
q.items.findAll { true }.each { q.cancel(it.task) }
```
 

## How to kill all the running jobs + any left in queue
```
 Jenkins.instance.queue.items.findAll { !it.task.name.contains("Extenda") }.each { 
  println "Cancel ${it.task.name}"
  Jenkins.instance.queue.cancel(it.task)
}
Jenkins.instance.items.each {
  stopJobs(it)
}
def stopJobs(job) {
  if (job in jenkins.branch.OrganizationFolder) {
    // Git behaves well so no need to traverse it.
    return
  } else if (job in com.cloudbees.hudson.plugins.folder.Folder) {
    job.items.each { stopJobs(it) }
  } else if (job in org.jenkinsci.plugins.workflow.multibranch.WorkflowMultiBranchProject) {
    job.items.each { stopJobs(it) }
  } else if (job in org.jenkinsci.plugins.workflow.job.WorkflowJob) {
    if (job.isBuilding() || job.isInQueue() || job.isBuildBlocked()) {
      job.builds.findAll { it.inProgress || it.building }.each { build ->
        println "Kill $build"
        build.finish(hudson.model.Result.ABORTED, new java.io.IOException("Aborted from Script Console"));
      }
    }
  }
}
```
