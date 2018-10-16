# EXAMPLE 6 PIPELINE: Job Outputs


Create pipeline:
  - on `linux` platform
  - using the `busybox` Docker container image
  - Task File is in Resources (`git`)
  - Task Script is in Resources (`git`)
  - Run Task Script from Resources (Some task that NOT only consumes an input resource and runs a script that runs some steps. But also creates some new output, that will be used as input for next step).
  
[Tutorial](https://concoursetutorial.com/basics/job-inputs/)


# RUN


## PREPARATION


**Git side**

This is a resource, which will be pointed.

Task Script `xbs_generate_output.sh` from resource.
```
#!/bin/sh

echo
echo "1) Current dir:"
pwd

echo
echo "2) Dirs before removing try (in current dir):"
ls -la 

echo 
echo "3) Removing output dir ..."
rm -rf output_dir

echo
echo "4) Dirs after removing try (in current dir):"
ls -la

echo 
echo "5) Creating output dir ..."
mkdir output_dir

echo
echo "6) Dirs after output creation try (in current dir):"
ls -la

echo
echo "7) Generating a file with date in output_dir ..."
echo > output_dir/curr_date.txt
date >> output_dir/curr_date.txt
echo >> output_dir/curr_date.txt


echo
echo "8) So all files after generating output (starting from curr dir):"
ls -la *

echo
echo
```

Task Script `xbs_get_generated_output.sh` from resource.
```
#!/bin/sh


echo
echo "1) Current dir:"
pwd

echo
echo "2) Dirs before getting output (current dir):"
ls -la

echo
echo "3) Getting generated output ..."

echo
cat output_dir/curr_date.txt
echo
echo
```

Don't forget to update your resource (`git` files in this case).
```
git add . && git commit -m "Playing with yml" && git push
```


**Local side**


This is where Task File with point to Resource is located.


Create Task File `xbs_local_task_file.yml` (`conc-pipeline` is the a dir IN repo, so NO REPO NAME).
```
---
resources:
- name: xbs_git_resource
  type: git
  source:
    uri: https://github.com/propalparolnapervom/test_dir.git
    branch: master

jobs:
- name: xbs_output_job
  public: true
  plan:
  - get: xbs_git_resource
  - task: xbs_generate_output_task
    config:
      platform: linux
      image_resource:
        type: docker-image
        source: {repository: busybox}

      inputs:
      - name: xbs_git_resource
      outputs:
      - name: output_dir

      run:
        path: xbs_git_resource/conc-pipeline/xbs_generate_output.sh

  - task: xbs_get_generated_output_task
    config:
      platform: linux
      image_resource:
        type: docker-image
        source: {repository: busybox}

      inputs:
      - name: xbs_git_resource
      - name: output_dir

      run:
        path: xbs_git_resource/conc-pipeline/xbs_get_generated_output.sh
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


## OUTPUT


Output of `xbs_generate_output_task` task:
```

1) Current dir:
/tmp/build/daf2749f

2) Dirs before removing try (in current dir):
total 16
drwxr-xr-x    4 root     root          4096 Oct 16 10:41 .
drwxr-xr-x    3 root     root          4096 Oct 16 10:41 ..
drwxr-xr-x    2 root     root          4096 Oct 16 10:41 output_dir
drwxr-xr-x    1 root     root          4096 Oct 16 10:41 xbs_git_resource

3) Removing output dir ...
rm: can't remove 'output_dir': Device or resource busy

4) Dirs after removing try (in current dir):
total 16
drwxr-xr-x    4 root     root          4096 Oct 16 10:41 .
drwxr-xr-x    3 root     root          4096 Oct 16 10:41 ..
drwxr-xr-x    2 root     root          4096 Oct 16 10:41 output_dir
drwxr-xr-x    1 root     root          4096 Oct 16 10:41 xbs_git_resource

5) Creating output dir ...
mkdir: can't create directory 'output_dir': File exists

6) Dirs after output creation try (in current dir):
total 16
drwxr-xr-x    4 root     root          4096 Oct 16 10:41 .
drwxr-xr-x    3 root     root          4096 Oct 16 10:41 ..
drwxr-xr-x    2 root     root          4096 Oct 16 10:41 output_dir
drwxr-xr-x    1 root     root          4096 Oct 16 10:41 xbs_git_resource

7) Generating a file with date in output_dir ...

8) So all files after generating output (starting from curr dir):
output_dir:
total 12
drwxr-xr-x    2 root     root          4096 Oct 16 10:41 .
drwxr-xr-x    4 root     root          4096 Oct 16 10:41 ..
-rw-r--r--    1 root     root            31 Oct 16 10:41 curr_date.txt

xbs_git_resource:
total 20
drwxr-xr-x    1 root     root          4096 Oct 16 10:41 .
drwxr-xr-x    4 root     root          4096 Oct 16 10:41 ..
drwxr-xr-x    9 root     root          4096 Oct 16 10:41 .git
drwxr-xr-x    3 root     root          4096 Oct 16 10:41 conc-pipeline
-rw-r--r--    1 root     root            17 Oct 16 10:41 readme.txt
```

Output of `xbs_get_generated_output_task` task:
```
1) Current dir:
/tmp/build/6ed60156

2) Dirs before getting output (current dir):
total 16
drwxr-xr-x    4 root     root          4096 Oct 16 10:41 .
drwxr-xr-x    3 root     root          4096 Oct 16 10:41 ..
drwxr-xr-x    1 root     root          4096 Oct 16 10:41 output_dir
drwxr-xr-x    1 root     root          4096 Oct 16 10:41 xbs_git_resource

3) Getting generated output ...


Tue Oct 16 10:41:04 UTC 2018
```



