# EXAMPLE_1 PIPELINE BASICS

Create pipeline:
  - on `linux` platform
  - using the `busybox` Docker container image
  - Task Script with command `uname -a`
  
[Tutorial](https://concoursetutorial.com/basics/basic-pipeline/)



# RUN

Pipeline file `pipeline.yml`:
```
---
jobs:
- name: job-hello-world
  public: true
  plan:
  - task: hello-world
    config:
      platform: linux
      image_resource:
        type: docker-image
        source: {repository: busybox}
      run:
        path: echo
        args: [hello world]
```

Set pipeline on that Task File:
```
fly -t tutorial set-pipeline -c pipeline.yml -p pipeline_xbs
```

































