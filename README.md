# OpenTracing

This repository contains the Docker build definition and release process for
a proof of concept about Zipkin in distributed mode.

## Regarding usage

There are six containers:

* MySQL (needed by Zipkin).
* Zipkin.
* Kafka (**Only in kafka branch**).
* Publisher application (_Microservice_).
* Formatter application (_Microservice_).
* Hello application (_Microservice_).

Hello is a main application which is responsible for the orchestration between
services, in this case a Formatter and Publisher. Formatter is a Java application
which receives an HTTP request with a name and returns _Hi, <name>_.
Publisher is a Java application which receives an HTTP request with a name and
says hello.

These modules, described above, send spans to a kafka instance. Kafka only have
to send the information to Zipkin.

**Note**: Hello, Formatter and Publisher application must be build running
`mvn clean package` command in theirs folders.

## Running

For that, only run `docker-compose up` in root of this repository where
it is the docker-compose.yml file.

## Testint

_Under construction_

```
$ curl 'http://localhost:8082/publish?helloStr=hi%20there'
$ curl 'http://localhost:8082/format?helloTo=Sergio'
```
