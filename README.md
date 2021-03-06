# elasticstack
ELK : elasticsearch + logstash + kibana

* Version : [5.0.1](https://github.com/easonlau02/elasticstack/tree/master/5.0.1)
* Version : [5.3.1](https://github.com/easonlau02/elasticstack/tree/master/5.3.1) + [docker-compose.yml for linux](https://github.com/easonlau02/elasticstack/blob/master/5.3.1/docker-compose.yml), [docker-compose.yml for docker_for_mac](https://github.com/easonlau02/elasticstack/blob/master/5.3.1/docker-compose.yml.docker_for_mac)
* Version : [5.6.3](https://github.com/easonlau02/elasticstack/tree/master/5.6.3) + [docker-compose.yml for linux](https://github.com/easonlau02/elasticstack/blob/master/5.6.3/docker-compose.yml), [docker-compose.yml for docker_for_mac](https://github.com/easonlau02/elasticstack/blob/master/5.6.3/docker-compose.yml.docker_for_mac)
* Version : [6.0.0](https://github.com/easonlau02/elasticstack/tree/master/6.0.0) + [docker-compose.yml for linux](https://github.com/easonlau02/elasticstack/blob/master/6.0.0/docker-compose.yml), [docker-compose.yml for docker_for_mac](https://github.com/easonlau02/elasticstack/blob/master/6.0.0/docker-compose.yml.docker_for_mac)
* Version : [6.1.2](https://github.com/easonlau02/elasticstack/tree/master/6.1.2) + [docker-compose.yml for linux](https://github.com/easonlau02/elasticstack/blob/master/6.1.2/docker-compose.yml), [docker-compose.yml for docker_for_mac](https://github.com/easonlau02/elasticstack/blob/master/6.1.2/docker-compose.yml.docker_for_mac)

Forwarder : filebeat port 5044

## Prerequisite

* OS : Centos 7.x
* Docker engine > 1.12.x
* Docker-compose > 1.11.x

## Clone GIT folder under your user home
    
    cd ~
    git clone https://github.com/easonlau02/elasticstack.git
## Now support 4 version for you to choose below way to up service
```bash
5.3.1/5.6.3/6.0.0/6.1.2
```
below take version 6.1.2 for example.

## The Simplest way to start all component:
1. Usage
```bash
cd ~/elasticstack/
chmod +x auto_up_elk_service.sh
./auto_up_elk_service.sh
usage: ./up_service.sh <linux|mac>  <5.3.1 5.6.3 6.0.1 6.1.2> <your_hostname>
```
* For linux user
```bash
./auto_up_elk_service.sh linux 6.1.2
```
* For Mac user
```bash
./auto_up_elk_service.sh mac 6.1.2 <your_hostname>
```
## The second way to start all component by version folder
1. Change config if you are using docker-for-mac under MAC
* Replace <your_es_host> with your running host for below config
```bash
~/elasticstack/6.1.2/docker-compose.yml.docker_for_mac
```
2. Startup ELK service at one machine
* For linux user
```bash
cd ~/elaticstack/6.1.2
docker-compose -f docker-compose.yml.linux up -d
```
* For Mac user
```bash
cd ~/elasticstack/6.1.2
docker-compose -f docker-compose.yml.docker_for_mac up -d
```
3. Access kibana via `<kibanahost>:5601`, you can see below screenshot
![alt text](https://raw.githubusercontent.com/easonlau02/elasticstack/master/6.0.0/kibana_up_status.png "kibana_up_status.png")
![alt text](https://raw.githubusercontent.com/easonlau02/elasticstack/master/6.1.2/kibana_up.png "kibana_up")

You can see **Unable to fetch mapping. Do you have indices match...**, caused by no log feed.
## HERE IS IMPORTANT!!!!
We managed all config file in images `eason02/elk-data-volume:6.1.2`, so if you need to change/add config for below folder.
```bash
~/elasticstack/6.1.2/elasticsearch/config/
~/elasticstack/6.1.2/logstash/config/
~/elasticstack/6.1.2/kibana/config/
```
And then run below related scripts to build new config image `eason02/elk-data-volume:6.1.2`.
```bash
cd ~/elasticstack/6.1.2/
chmod +x build_data_volumes_for_elk.sh
./build_data_volumes_for_elk.sh
```
Restart elk service to take effect.
* For linux user:
```bash
cd ~/elasticstack/6.1.2/
docker-compose -f docker-compose.yml.linux restart
```
* For Mac user:
```bash
cd ~/elasticstack/6.1.2/
docker-compose -f docker-compose.yml.docker_for_mac restart
```

## Feedback and new requirement
1. Fork it (https://github.com/easonlau02/elasticstack/fork)
2. Comment below/requirement or [raise issue](https://github.com/easonlau02/elasticstack/issues)
