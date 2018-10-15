# CONCOURSE COMMANDS

[Tutorial](https://concoursetutorial.com/)


# START/STOP

> For the case when Concourse is deployed via Docker Compose

> From the directory, where Docker Compose file for Concourse was placed

**Up**

(create new containers and start them)
```
docker-compose up -d
```

**Down** 

(stop containers and destroy them)
```
docker-compose down
```

**Start** 

(start already existing containers)
```
docker-compose start
```

**Stop**

(just stop containers, without their destroing)
```
docker-compose start
```


# TARGET

Set `tutorial` alias for the target.
```
fly --target tutorial login --concourse-url http://127.0.0.1:8080 -u admin -p admin
```

Sync `tutorial` target.
```
fly --target tutorial sync
```

See saved targets
```
cat ~/.flyrc
```

# TASK

Run `example.yml` task file on `tutorial` target.
```
fly -t tutorial e -c example1.yml
```

# INPUTS

`input` defines content of **working folder** inside the container.

_______________

Use current dir as `input`
```
fly -t tutorial e -c inputs_required.yml -i some-important-input=.
```

To pass in a different dir as an `input`
```
fly -t tutorial e -c inputs_required.yml -i some-important-input=../task-hello-world
```

The `fly execute -i` option can be removed if the current dir is the same name as the required input.



# PIPELINE

## SET

Set pipeline `pl_xbs` from `pl_xbs.yml` pipeline file.
```
fly -t tutorial set-pipeline -c pl_xbs.yml -p pl_xbs

fly -t tutorial sp -c pl_xbs.yml -p pl_xbs
```

## PAUSE/UNPAUSE

Unpause whole `pipeline_xbs` pipeline.
```
fly -t tutorial unpause-pipeline -p pipeline_xbs

fly -t tutorial up -p pipeline_xbs
```

Unpause only `job_xbs` job in `pipeline_xbs` pipeline.
```
fly -t tutorial unpause-job --job pipeline_xbs/job_xbs

fly -t tutorial uj --job pipeline_xbs/job_xbs
```

___________

Pause whole `pipeline_xbs` pipeline.
```
fly -t tutorial pause-pipeline -p pipeline_xbs

fly -t tutorial pp -p pipeline_xbs
```

Pause only `job_xbs` job in `pipeline_xbs` pipeline.
```
fly -t tutorial pause-job --job pipeline_xbs/job_xbs

fly -t tutorial pj --job pipeline_xbs/job_xbs
```



## DESTROY

Destroy `pl_xbs` pipeline.
```
fly -t tutorial destroy-pipeline -p pl_xbs 

fly -t tutorial dp -p pl_xbs
```


# JOB

## LIST RUNS


Sho jobs runs
```
fly -t tutorial builds

fly -t tutorial builds -j xbs_local_pipeline/xbs_local_job
```


## OUTPUT

Show the output of LATEST run of `xbs_local_job` job from `xbs_local_pipeline` pipeline.
```
fly -t tutorial watch -j xbs_local_pipeline/xbs_local_job
```

Show the output of run #5 of `xbs_local_job` job from `xbs_local_pipeline` pipeline.
```
fly -t tutorial watch --build 5 -j xbs_local_pipeline/xbs_local_job
```


## TRIGGER

Trigger job from command line
```
fly -t tutorial trigger-job -j xbs_local_pipeline/xbs_local_job
```

Trigger job and watch it simualteneously
```
fly -t tutorial trigger-job -j xbs_local_pipeline/xbs_local_job -w
```












