# Apache Kafka - Docker Image

# docker-compose images

This project uses the following images:

**Kafka:**  confluentinc/cp-kafka  
**Zookeper:** confluentinc/cp-zookeeper:latest
**kafka-ui**: provectuslabs/kafka-ui:latest

# Confluentic - cp-kafka

## Kafka Path

```
/etc/kafka
```

## confluentinc - configuration

## Replicas

For ssl_plaintext config needs three broker. 

**Needs to check if configuration must be tailored for 1 broker **

# Docker

## Run

```
docker-compose -f .\docker-compose.yml up
```

```
docker-compose -f .\docker-compose-with-topic-init.yml up
```

```
docker-compose -f .\docker-compose-with-topic-init-with-jmx.yml up
```

```
docker-compose -f .\docker-compose-with-topic-init-with-jmx-with-monitoring.yml up
```

## Stop

```
docker-compose -f .\docker-compose.yml down
```

```
docker-compose -f .\docker-compose-with-topic-init.yml down
```

```
docker-compose -f .\docker-compose-with-topic-init-with-jmx.yml down
```

## Clean images

```
docker system prune -af --volumes
```

# Monitoring UI

## Prometheus

**URL:** http://localhost:9090

## Grafana

**URL:** http://localhost:3000

# Springboot YML configuration with docker
