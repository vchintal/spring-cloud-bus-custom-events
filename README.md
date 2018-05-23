# Custom Events using spring-cloud-bus with AMQ Artemis

Sample application to demonstrate how to publishing custom events using Spring Cloud Bus via AMQ Artemis

## Prerequisites

* Git clone this project onto your local machine
* Download the [AMQ Artemis binary](https://developers.redhat.com/download-manager/file/amq-broker-7.1.1-bin.zip) and unzip it. Let us call the full path to the folder `amq-broker-7.1.0` as `ARTEMIS_HOME`
* Run the following command to create a broker instance at a location of your choice and follow the instructions displayed with username `admin`, password `admin` and choose `Y` for allow-anonymous
  ```sh
  $ARTEMIS_HOME/bin/artemis create mybroker
  ```
* Reset the `$ARTEMIS_HOME` to full path to the `mybroker` instance and run the following command to run the Artemis instance 
  ```sh 
  $ARTEMIS_HOME/bin/artemis run
  ```
*  The admin console can now be opened here : http://localhost:8161/console

## Run the demo

### Launch instance one
From the root folder of this project run the following command:
```sh 
mvn spring-boot:run 
```
### Launch instance two
From the root folder of this project run the following command:
```sh 
mvn spring-boot:run -Dserver.port=8081
```
### Hit a REST endpoint on instance one to generate the custom event
```sh 
curl -X POST localhost:8080/publish
```

If everything was working correctly, you should see the following response for the REST call 

```sh
event published
```

## Test Results 

As a result of the REST call you should a log entry that looks something like the one shown below on either instances 

```sh
2018-05-23 09:45:50.493  INFO 26304 --- [nio-8080-exec-1] c.t.example.MyCustomRemoteEventListener  : Received MyCustomRemoteEvent - message: hello world
```