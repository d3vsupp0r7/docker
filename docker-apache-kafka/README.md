- [Confluentic - Kafka - Docker Example](#confluentic---kafka---docker-example)
  - [Verison](#verison)
  - [URL](#url)
- [Kafka - UI](#kafka---ui)
  - [Kafka standalone UI](#kafka-standalone-ui)
- [Confluentic Kafka config](#confluentic-kafka-config)
  - [Init topics  on docker startup - to test](#init-topics--on-docker-startup---to-test)
    - [template](#template)
    - [test working - no message autocreation](#test-working---no-message-autocreation)
    - [INIT TOPIC ON STARTUP](#init-topic-on-startup)
  
# Confluentic - Kafka - Docker Example

## Verison

cd /bin
kafka-broker-api-versions --version

## URL
https://docs.confluent.io/platform/current/release-notes/index.html

# Kafka - UI

## Kafka standalone UI

Kfka too must use port 29092

https://www.kafkatool.com/

# Confluentic Kafka config
## Init topics  on docker startup - to test
### template
 kafka-init-topics:
    image: confluentinc/cp-kafka:5.3.1
    volumes:
       - ./message.json:/data/message.json
    depends_on:
      - kafka1
    command: "bash -c 'echo Waiting for Kafka to be ready... && \
               cub kafka-ready -b kafka1:29092 1 30 && \
               kafka-topics --create --topic second.users --partitions 3 --replication-factor 1 --if-not-exists --zookeeper zookeeper1:2181 && \
               kafka-topics --create --topic second.messages --partitions 2 --replication-factor 1 --if-not-exists --zookeeper zookeeper1:2181 && \
               kafka-topics --create --topic first.messages --partitions 2 --replication-factor 1 --if-not-exists --zookeeper zookeeper0:2181 && \
               kafka-console-producer --broker-list kafka1:29092 -topic second.users < /data/message.json'"

### test working - no message autocreation

 ### INIT TOPIC ON STARTUP
  init-kafka:
    image: confluentinc/cp-kafka:latest
    depends_on:
      - kafka0
    entrypoint: [ '/bin/sh', '-c' ]
    command: |
      "
      # blocks until kafka is reachable
      kafka-topics --bootstrap-server kafka0:9092 --list

      echo -e 'Creating kafka topics'
      kafka-topics --bootstrap-server kafka0:9092 --create --if-not-exists --topic my-topic-1 --replication-factor 1 --partitions 1
      kafka-topics --bootstrap-server kafka0:9092 --create --if-not-exists --topic my-topic-2 --replication-factor 1 --partitions 1

      echo -e 'Successfully created the following topics:'
      kafka-topics --bootstrap-server kafka0:9092 --list
      "