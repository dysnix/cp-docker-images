## https://docs.docker.com/docker-hub/builds/advanced/
ARG GIT_BRANCH
FROM confluentinc/cp-kafka-connect:$GIT_BRANCH

## In the tag version has an ordinal suffix we wipe it out  (5.3.1-1 => 5.3.1)
ARG GIT_BRANCH
RUN confluent-hub install --no-prompt confluentinc/kafka-connect-jdbc:${GIT_BRANCH%-*} && \
  confluent-hub install --no-prompt debezium/debezium-connector-sqlserver:0.10.0
