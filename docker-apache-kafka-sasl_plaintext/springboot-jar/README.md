# Springboot to use kafka sasl configuration

# Run spring boot app

The springboot will run on port: 8081

```
java -jar springboot2-kafka-sasl-0.0.1-SNAPSHOT.jar
```

## Use of external yml file for springboot

```
java -jar springboot2-kafka-sasl-0.0.1-SNAPSHOT.jar --spring.config.location=filename.yml
```


# Use postman to produce message

Use request: sendJSONMessage