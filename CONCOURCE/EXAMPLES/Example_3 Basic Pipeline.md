# EXAMPLE_3 Basic Pipeline

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

Set pipeline on that pipefile:
```
fly -t tutorial set-pipeline -c pipeline.yml -p pipeline_xbs

      pipeline created!
      you can view your pipeline here: http://127.0.0.1:8080/teams/main/pipelines/pipeline_xbs

      the pipeline is currently paused. to unpause, either:
        - run the unpause-pipeline command
        - click play next to the pipeline in the web ui
```

































