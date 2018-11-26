
You have tagged workers in Concourse.

Pin your Pipeline to specific worker with `cicd` tag:
```
  ...
  - task: "build_release_to_del2"
    tags: [cicd]
    image: node8
    config:
  ...
```
