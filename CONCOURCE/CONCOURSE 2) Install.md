# CONCOURSE INSTALL


## MANUAL INSTALLATION

### DOWNLOAD

[Download](https://concourse-ci.org/download.html)


### INSTALL

[Install](https://concourse-ci.org/install.html)




## DEPLOYMENT VIA DOCKER COMPOSE

[Tutorial](https://concoursetutorial.com/)

**Docker** and **Docker Copmose** have to be installed.


### PREPARATION

Create a dir where Docker Compose `yaml` file will be downloaded
```
mkdir -p ~/init_install/concourse_via_dock
```

Download compose-file
```
cd ~/init_install/concourse_via_dock
wget https://raw.githubusercontent.com/starkandwayne/concourse-tutorial/master/docker-compose.yml
```

### START/STOP CONCOURSE



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


### POST-INSTALLATION

Test installation:  [http://127.0.0.1:8080/](http://127.0.0.1:8080/)


Click on necessary OS to download `fly` CLI.


Once downloaded - make it executable, copy to your PATH
```
sudo mv ~/Downloads/fly /usr/local/bin
sudo chmod 0755 /usr/local/bin/fly
ls -la /usr/local/bin/fly
```










