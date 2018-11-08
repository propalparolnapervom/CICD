# CONCOURSE OVERALL

[Docs: Overall](https://concourse-ci.org/index.html)

[Tutorial: Basics](https://concoursetutorial.com/)

[Tutorial: Miscellaneous](https://concoursetutorial.com/miscellaneous/)


## TASKS

The central concept of Concourse is to run **tasks**. You can run them:
  - directly from the command line
  - from within pipeline jobs

Every task in Concourse runs within a "container" (as best available on the target platform).


## INPUTS

[Tutorial](https://concoursetutorial.com/basics/task-inputs/)

In the previous section the only inputs to the task container were the `image` used. 

Base images, such as Docker images, are relatively static and relatively big, slow things to create. 

So Concourse supports `inputs` into tasks to pass in files/folders for processing.


Consider the **working directory** of a task that explicitly has no inputs:

```
cd ../task-inputs
fly -t tutorial e -c no_inputs.yml
```

The task runs `ls -al` to show the (empty) contents of the **working folder** inside the container:
```
      running ls -al
      total 8
      drwxr-xr-x    2 root     root          4096 Feb 27 07:23 .
      drwxr-xr-x    3 root     root          4096 Feb 27 07:23 ..
```

Commonly if wanting to run `fly` execute we will want to pass in the local folder `(.)`. Use `-i name=path` option to configure each of the required `inputs`:
```
fly -t tutorial e -c inputs_required.yml -i some-important-input=.
```

Now the `fly` execute command will upload the `.` directory as an input to the container.

To pass in a different directory as an input, provide its absolute or relative path:
```
fly -t tutorial e -c inputs_required.yml -i some-important-input=../task-hello-world
```

The `fly execute -i` option can be removed if the current directory is the same name as the required input.

___________

The `inputs` feature of a task allows us to pass in two types of inputs:
  - **requirements/dependencies** to be processed/tested/compiled
  - **task scripts** to be executed to perform complex behavior



## RESOURCES

[Tutorial](https://concoursetutorial.com/basics/pipeline-resources/)

[Docs: Resources](https://concourse-ci.org/resources.html)

[Docs: Resource Types](https://concourse-ci.org/resource-types.html)

[List of Default resources](https://concourse-ci.org/included-resources.html)

With **pipelines** we need to store the **task file** and **task script** somewhere outside of Concourse.

Concourse offers no services for storing/retrieving your data. No git repositories. No blobstores. No build numbers. 

Every input and output must be provided externally. Concourse calls them **Resources**. 

Example resources are:
  - git
  - s3
  - semver


## STEPS

### PUT

**Why does Concourse `get` a resource after `put`ing it?**

Every `put` implies a `get` of the version that was created. There are a few reasons for this:

The primary reason for this is so that the newly created resource can be used by later steps in the build plan. Without the `get` there is no way to introduce "new" resources during a build's execution, as they're all resolved to a particular version to fetch when the build starts.

There are some side-benefits to doing this as well. For one, it immediately warms the cache on one worker. So it's at least not totally worthless; later jobs won't have to fetch it. It also acts as validation that the put actually had the desired effect.

In this particular case, as it's the last step in the build plan, the primary reason doesn't really apply. But we didn't bother optimizing it away since in most cases the side benefits make it worth not having the secondary question arise ("why do only SOME put steps imply a get?").

It also cannot be disabled as we resist adding so many knobs that you'll want to turn one day and then have to go back and turn back off once you actually do need it back to the default.




























