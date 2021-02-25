# Kafka on Docker
This project is used to set up the Kafka cluster for development. The image is `wurstmeister/kafka:2.12-2.5.0` available in Dockerhub.

## Details
By running "`docker-compose up`" or "`docker-compose up -d`", you will get a Kafka cluster of 3 brokers. Important configurations include

```bash
# The interface that the broker binds to
KAFKA_LISTENERS: INTERNAL://:9093,EXTERNAL://:9092
# The interface exposed to the client (The client will use this configuration to connect to the broker)
KAFKA_ADVERTISED_LISTENERS: INTERNAL://:9093,EXTERNAL://localhosy:9092
# The rest of the configuration can be found in the "docker-compose.yml" file
.....
```

To explain above configuration, the listeners are splitted into `internal` and `external` listeners. For inter-broker communication, the `INTERNAL` listener is used while `EXTERNAL` listener is used for clients outside Docker.

### Notes
- This project is meant to be used for development only
- Consider using Docker Volume to persist the data so the brokers retain its information and offsets across server(container) restarts
- For production deployment, I highly recommend running the brokers in virtual machines instead of Docker container as it is easier to manage the brokers