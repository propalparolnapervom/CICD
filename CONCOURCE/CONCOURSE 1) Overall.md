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






























