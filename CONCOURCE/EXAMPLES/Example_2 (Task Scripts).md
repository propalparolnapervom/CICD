# EXAMPLE_2 Task Scripts

Run task file from command line:
  - on `linux` platform
  - using the `busybox` Docker container image
  - Task Script with command `uname -a`
  
  
# RUN

Task script `task_show_uname.sh`:
```
#!/bin/sh

uname -a
```

Task file `task_show_uname.yml`
```
---
platform: linux

image_resource:
  type: docker-image
  source: {repository: busybox}

inputs:
- name: task-scripts

run:
  path: ./task-scripts/task_show_uname.sh
```

Run
```
fly -t tutorial e -c task_show_uname.yml
```






















