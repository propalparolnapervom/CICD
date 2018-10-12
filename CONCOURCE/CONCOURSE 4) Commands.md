# CONCOURCE COMMANDS

[Tutorial](https://concoursetutorial.com/)


## START/STOP

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


## TARGET

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

































