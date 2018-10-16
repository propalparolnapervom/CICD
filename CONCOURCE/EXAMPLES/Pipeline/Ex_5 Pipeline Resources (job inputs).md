# EXAMPLE 5 PIPELINE RESOURCES (job input)


Create pipeline:
  - on `linux` platform
  - using the `busybox` Docker container image
  - Task File is in Resources (`git`)
  - Task Script is in Resources (`git`)
  - Run Task Script from Resources
  
[Tutorial](https://concoursetutorial.com/basics/job-inputs/)


# RUN


## PREPARATION


**Git side**

This is a resource, which will be pointed.

Task Script `xbs_resource_task_script.sh` from resource.
```
#!/bin/sh

echo
echo "This is TASK SCRIPT from RESOURCE!"
echo
```


Task File `xbs_resource_task_file.yml` from resource (`conc-pipeline` is the a dir IN repo, so NO REPO NAME).
```
---
platform: linux

image_resource:
  type: docker-image
  source: {repository: golang, tag: 1.9-alpine}

inputs:
- name: xbs_local_resource

run:
  path: xbs_local_resource/conc-pipeline/xbs_resource_task_script.sh
```



**Local side**


This is where Task File with point to Resource is located.

Create Task File `xbs_local_task_file.yml` (`conc-pipeline` is the a dir IN repo, so NO REPO NAME).
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







