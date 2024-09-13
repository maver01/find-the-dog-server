# Find the dog server

This repository contains the code related to the server, handling the requests of image processing from the frontend, for the find-the-dog project. It is only meant for learning purposes.

## Description

The code handles the the requests from the frontend, by implementing an API that can receiving images from the post requests at frontend, and redirecting them to a queueing system through a kafka topic, that is later processed by an independent python microservice module that process the images. The processed images are then received by consuming from a second kafka topic and made available to the frontend through API request.

Main directory tree:

```
├── pom.xml
├── src
│   ├── main
│   │   ├── java
│   │   │   └── com
│   │   │       └── findTheDog
│   │   │           └── app
│   │   │               ├── App.java
│   │   │               ├── ImageController.java
│   │   │               ├── KafkaImageConsumer.java
│   │   │               └── KafkaImageProducer.java

```

## Understand the code

- KafkaImageProducer: Receives the image from the frontend, through POST API request, then sends the image as byte stream to the kafka topic, for it to be handles by the independent processing microservice.
- KafkaImageConsumer: Consumes the processed images produced by the independent processing microservice.
- ImageController: Sends the processed image to the frontend, through API request.

 Post request handling and kafka producer are syncronous services. Kafka consumer and GET service are asyncronous.

## Run the code

Assuming maven, java and spring-boot are installed, and kafka and zookeeper are running (see additional documentation under _docs_), run:

```
mvn spring-boot:run
```
