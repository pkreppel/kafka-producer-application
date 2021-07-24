# Projeto Kafka Consumer
--Projeto criado seguindo tutorial do site Karfka confluent.
https://kafka-tutorials.confluent.io/creating-first-apache-kafka-producer-application/confluent.html

## Criar containers kafka
docker-compose up -d

## Criar um tópico manualmente
docker-compose exec broker bash
kafka-topics --create --topic output-topic --bootstrap-server broker:9092 --replication-factor 1 --partitions 1

## Compilar e executar com o gradle
./gradlew shadowJar
java -jar build/libs/kafka-producer-application-standalone-0.0.1.jar configuration/dev.properties input.txt

## Teste com gradle
./gradlew test

## Criar uma imagem
gradle jibDockerBuild --image=io.confluent.developer/kafka-producer-application-join:0.0.1

## Executar o container
docker run -v $PWD/configuration/prod.properties:/config.properties io.confluent.developer/kafka-producer-application-join:0.0.1 config.properties
