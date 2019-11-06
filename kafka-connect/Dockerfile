# https://docs.docker.com/docker-hub/builds/advanced/
ARG DOCKER_TAG
FROM confluentinc/cp-kafka-connect:$DOCKER_TAG
RUN confluent-hub install --no-prompt debezium/debezium-connector-postgresql:0.10.0 && \
  confluent-hub install --no-prompt confluentinc/kafka-connect-jdbc:5.3.1
