FROM maven:3.6-jdk-8 AS build

ARG RELEASE
RUN \
  git clone -b uuid-5.2.0 https://github.com/dysnix/kafka-connect-jdbc.git && \
  cd kafka-connect-jdbc && \
  git remote add upstream https://github.com/confluentinc/kafka-connect-jdbc.git && \
  ## only X.y.z releases of kafka connect are expected (v5.2.0, v5.3.1 etc) \
  git fetch upstream v"${RELEASE%%-*}" && \
  git checkout FETCH_HEAD && \
  git config --local user.email "root@localhost" && \
  git cherry-pick $(git rev-list uuid-5.2.0 -1) && \
  sed -i 's~<url>${confluent.maven.repo}</url>~<url>https://packages.confluent.io/maven/</url>~' pom.xml && \
  mvn package -Dmaven.test.skip

## https://docs.docker.com/docker-hub/builds/advanced/
ARG RELEASE
FROM confluentinc/cp-kafka-connect:$RELEASE

## In the tag version has an ordinal suffix we wipe it out  (5.3.1-r1 => 5.3.1)
ARG RELEASE
RUN confluent-hub install --no-prompt debezium/debezium-connector-sqlserver:0.10.0

## Install custom jars
COPY --from=build /kafka-connect/target/kafka-connect-jdbc-"${RELEASE%%-*}".jar /etc/kafka-connect/jars/
