ARG SOURCE_REF
FROM confluentinc/cp-kafka-connect:$SOURCE_REF
RUN confluent-hub install --no-prompt debezium/debezium-connector-postgresql:0.10.0 && \
  confluent-hub install --no-prompt confluentinc/kafka-connect-jdbc:5.3.1
