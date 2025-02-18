# Elastic and Kibana Docker Setup

This document provides instructions on how to set up Elasticsearch and Kibana using Docker.

## Docker Compose Configuration

Below is the Docker Compose configuration to set up Elasticsearch and Kibana:

## Services

- **es8**: Elasticsearch service

  - Image: `docker.elastic.co/elasticsearch/elasticsearch-wolfi:8.17.2`
  - Ports: `9200:9200`
  - Environment Variables:
    - `node.name=es8`
    - `cluster.name=es-docker-cluster`
    - `discovery.type=single-node`
  - Volumes:
    - `data:/usr/share/elasticsearch/data`

- **kib8**: Kibana service
  - Image: `docker.elastic.co/kibana/kibana:8.17.2`
  - Ports: `5601:5601`
  - Environment Variables:
    - `ELASTICSEARCH_HOSTS=http://es8:9200`
  - Depends on: `es8`

## Volumes

- **data**: Persistent storage for Elasticsearch data

## Networks

- **elastic**: Custom bridge network for communication between services

## Set password

````
    docker exec --user='root' -it es8 /bin/bash
    cd config/
    nano elasticsearch.yml

    ```
    # Enable security features
    xpack.security.enabled: false

    xpack.security.enrollment.enabled: false

    ```
````

## Stop and Run again

```
docker compose up --build
```

## Link

    - http://localhost:9200/  [Elastic Search]
    - http://localhost:5601/  [Kibana]

For more information, refer to:

[![Docker](https://img.shields.io/badge/Get%20Started-Docker-blue?logo=docker)](https://www.docker.com/get-started/)  
[![Elasticsearch](https://img.shields.io/badge/Elasticsearch-Docker-orange?logo=elasticsearch)](https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html)  
[![Kibana](https://img.shields.io/badge/Kibana-Docker-green?logo=kibana)](https://www.elastic.co/guide/en/kibana/current/docker.html)


## Process

<img width="1171" alt="Screenshot 2025-02-18 at 11 00 49 in the morning" src="https://github.com/user-attachments/assets/684d6791-88da-4c46-8737-1338dbe929d4" />
