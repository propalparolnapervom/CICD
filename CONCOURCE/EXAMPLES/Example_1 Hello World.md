# EXAMPLE_1 Hello World

Run task from command line:
  - on `linux` platform
  - using the `busybox` Docker container image
  - command `echo`
  
[Tutorial](https://concoursetutorial.com/basics/task-hello-world/)
  
# RUN

Create `example1.yml` task file.
```
mkdir /Users/sbur/overall/test/example1
cd /Users/sbur/overall/test/example1
touch example1.yml
```

Update `example1.yml` task file.
```
---
platform: linux

image_resource:
  type: docker-image
  source: {repository: busybox}

run:
  path: echo
  args: [hello world]
```

OR (another way to define arguments)

```
---
platform: linux

image_resource:
  type: docker-image
  source: {repository: busybox}

      run:
        path: sh
        args: 
          - "-ec"
          - |
            ls -la
            pwd
            uname -a
            echo
            echo "git version is"
            git --version
```

Run task
```
fly -t tutorial e -c example1.yml
```

Check result [http://127.0.0.1:8080/builds/1](http://127.0.0.1:8080/builds/1)














