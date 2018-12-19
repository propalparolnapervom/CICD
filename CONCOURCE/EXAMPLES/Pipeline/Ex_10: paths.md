# WHAT

Make pipeline that triggers on specific dir in repo only (instead of whole repo) and ckeouts whole repo.

## CODE


This is repo:
```
-rw-r--r--   1 sbur  staff   17 Dec 17 16:11 additional_file.txt
drwxr-xr-x   7 sbur  staff  224 Dec 17 15:34 conc-pipeline
-rw-r--r--   1 sbur  staff   17 Dec 17 15:34 readme.txt
ip-172-29-230-10:test_dir sbur$ pwd
/Users/sbur/overall/git_area/test_dir
```

This is pipeline:
```
---
jobs:
- name: build
  public: true
  plan:
  - aggregate: # Get all dependencies in parallel
    - get: xbs_local_resource
      trigger: true
  - task: "xbs_task"
    config:
      platform: linux
      image_resource:
        type: docker-image
        source:
          repository: cypress/base
          tag: 8
      inputs:
      - name: xbs_local_resource
      caches:
      - path: ~/.cache
      run:
        path: sh
        args:
          - "-ec"
          - |
            echo
            echo Checkouted
            ls -la ; pwd

            echo
            echo cd xbs_local_resource
            cd ./xbs_local_resource ; ls -la ; pwd



resources:
- name: xbs_local_resource
  type: git
  source:
    uri: https://github.com/propalparolnapervom/test_dir.git
    branch: master
    paths: 
          - './conc-pipeline/output_dir'

```

## RESULTS

### Changing not submodule

Changing of the any other file, but not one in `conc-pipeline/output_dir` dir.

Nothing is hapenning: pipeline is not triggered.

### Changing submodule

Changing file in `conc-pipeline/output_dir` dir.

Pipeline is triggering.

Whole repo will be checkouted as `xbs_local_resource` resource (not submodule)



