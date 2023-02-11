# Introduction

In this gist, we will quickly try to spin Elastic stacks with Docker containers. We are going to use [docker-compose](https://docs.docker.com/compose/). You can learn more about [Docker](https://www.docker.com/) & [Docker Compose](https://docs.docker.com/compose/), Which will help you to understand the flow.  

# Prerequisite

Tested on the below configuration.

* docker:`Docker version 20.10.16, build aa7e414`
* docker-compose:`Docker version 20.10.16, build aa7e414`

# Cluster

This setup will include

- [x] Elasticsearch
- [x] Kibana
- [x] Logstash
- [x] APM

# Setup

Clone repo:

```sh
git clone https://github.com/ashishtiwari1993/elastic-docker.git
cd elastic-docker
``` 

Make changes in `.env` file.

# Start the cluster

## Start

```sh
docker-compose up -d
```

Just visit to `localhost:5601`. You should see a kibana login page. 

## Stop

```sh
docker-compose down
```

## Stop with deleting network, containers and volumes

```sh
docker-compose down -v
```

# Access stacks

## Elasticsearch

### Access via `curl` from host machine

#### Copy `ca.crt` file

```sh
docker cp elastic-docker_es01_1:/usr/share/elasticsearch/config/certs/ca/ca.crt /tmp/
```

#### Curl command

```sh
curl --cacert /tmp/ca.crt -u elastic:pass@123 https://localhost:9200
```

## Logstash

1. You need to have pipeline configuration files on `LOGSTASH_PIPELINE_PATH` location. If there will be no file, Logstash will throw an error and get exit.

# NOTE 

> You can simply comment other stacks which is not needed. For example if you want to just run Elasticsearch & Kibana, Just comment the APM or other stack specification.
