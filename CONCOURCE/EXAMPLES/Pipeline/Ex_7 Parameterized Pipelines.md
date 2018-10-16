# EXAMPLE 7 PIPELINE: Parameterized Pipelines



Create pipeline:
  - on `linux` platform
  - using the `busybox` Docker container image
  - Task File is in Resources (`git`)
  - Task Script is in Resources (`git`)
  - Run Task Script from Resources with parametrized values
  
[Tutorial](https://concoursetutorial.com/basics/parameters/)


# RUN


## PREPARATION


Task File `pipeline.yml`, with parameters that define:
  - variables `CAT_NAME` and `DOG_NAME` in the Docker container;


```
---
jobs:
- name: show-animal-names
  plan:
  - task: show-animal-names
    config:
      platform: linux
      image_resource:
        type: docker-image
        source: {repository: busybox}
      run:
        path: env
        args: []
      params:
        CAT_NAME: ((cat-name))
        DOG_NAME: ((dog-name))
```


## DEFINE PARAMETERS (OPTION 1)

Parameters via `fly` keys.
```
fly -t tutorial sp -p parameters -c pipeline.yml -v cat-name=garfield -v dog-name=odie
```


## DEFINE PARAMETERS (OPTION 2)

Parameters via separate file.

Create a file `credentials.yml` with necessary parameters defined
```
echo "cat-name: olya" > credentials.yml
echo "dog-name: kolya" >> credentials.yml
```

Use `--load-vars-from` (aliased `-l`) key to pass this file to `fly` utility
```
fly -t tutorial sp -p parameters -c pipeline.yml -l credentials.yml
```

> NOTE: There are two downsides to the two approaches above.

> 1) To change any parameter values requires you to rerun fly set-pipeline. If a value is common across many pipelines then you must rerun fly set-pipeline for them all.
> 2) The parameter values are not very secret. Anyone with access to the pipeline's team is able to download the pipeline YAML and extract the secrets.















