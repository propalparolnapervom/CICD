# EXAMPLE_4 PIPELINE RESOURCES (trigger on time)

[Time Docs](https://github.com/concourse/time-resource)

Create pipeline:
  - on `linux` platform
  - using the `busybox` Docker container image
  - Task File is in Resources (`git`)
  - Task runs  every 1 min
  
[Tutorial](https://concoursetutorial.com/basics/triggers/)


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
  args: [This was pulled out in time interval]
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

- name: timer
  type: time
  source:
      start: 10:30 AM
      stop: 10:35 AM
      location: Europe/London
    
jobs:
- name: xbs_local_job
  public: true
  plan:
  - get: xbs_local_resource
  - get: xbs_timer
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


































