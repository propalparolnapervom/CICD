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

**Set**

Set pipeline `pl_xbs` from `pl_xbs.yml` pipeline file.
```
fly -t tutorial set-pipeline -c pl_xbs.yml -p pl_xbs

fly -t tutorial sp -c pl_xbs.yml -p pl_xbs
```


**Unpause**

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

**Pause**

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























