# EXAMPLE_3 PIPELINE RESOURCES (trigger on commit)

Create pipeline:
  - on `linux` platform
  - using the `busybox` Docker container image
  - Task File is in Resources (`git`)
  - Task runs each time Resource (`git`) is updated
  
[Tutorial](https://concoursetutorial.com/basics/pipeline-resources/)


# RUN


## PREPARATION


**Git side**

This is a resource, which will be pointed.


Task File `xbs_resource_task_file.yml` from resource.
```
---
platform: linux

image_resource:
  type: docker-image
  source: {repository: busybox}

run:
  path: echo
  args: [This was pulled out from the Git]
```



**Local side**


This is where Task File with point to Resource is located.

Create Task File `xbs_local_task_file.yml`
```
resources:
- name: xbs_local_resource
  type: git
  source:
    uri: https://github.com/propalparolnapervom/test_dir.git
    branch: master
    
jobs:
- name: xbs_local_job
  public: true
  plan:
  - get: xbs_local_resource
    trigger: true
  - task: xbs_local_task
    file: xbs_local_resource/conc-pipeline/xbs_resource_task_file.yml 
```


## SET PIPELINE


Create `xbs_local_pipeline` pipeline on `xbs_local_task_file.yml`:
```
fly sp -t tutorial -c xbs_local_task_file.yml -p xbs_local_pipeline
```

Unpause whole `xbs_local_pipeline` pipeline.
```
fly -t tutorial up -p xbs_local_pipeline
```


































