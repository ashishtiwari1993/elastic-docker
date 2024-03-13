# Introduction

In this gist, we will quickly try to spin Elastic stacks with Docker containers. We are going to use [docker-compose](https://docs.docker.com/compose/). You can learn more about [Docker](https://www.docker.com/) & [Docker Compose](https://docs.docker.com/compose/), Which will help you to understand the flow.  

# Prerequisite

Tested on the below configuration.

* docker:`Docker version 20.10.16, build aa7e414`
* docker-compose:`Docker version 20.10.16, build aa7e414`

# Cluster

This setup will include

- ✅ Elasticsearch
- ✅ Kibana
- ✅ Logstash
- ✅ APM Server

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
docker cp elastic-docker-es01-1:/usr/share/elasticsearch/config/certs/ca/ca.crt /tmp/
```

#### Curl command

```sh
curl --cacert /tmp/ca.crt -u elastic:pass@123 https://localhost:9200
```

## Logstash

### Pipeline config files

Place all `*.conf` files in `logstash_external_configs/pipeline/`. You can create folder and files in `logstash_external_configs` which will get mounted on `/usr/share/logstash/logstash_external_configs` in container.

### Installing plugin

Either you can add in `docker-compose.yml` file or you can simply run command like below while container is up.

```sh
docker exec -it elastic-docker-logstash-1 bin/logstash-plugin install logstash-output-google_pubsub
```


# NOTE 

> You can simply comment other stacks which is not needed. For example if you want to just run Elasticsearch & Kibana, Just comment the APM or other stack specification.
