# KSQL
conversion to cannonical model using ksql

## Steps to use ksql

### STEP1
`cd` to `confluent-5.4.x`
start the ksql server using `./bin/ksql-server-start ./etc/ksql/ServerConfig.properties`

### STEP2
start kafka console usign `./bin/ksql http://localhost:8088`

### STEP3
create a stream from existing topic using `for example: CREATE STREAM ksql_csv_issue WITH (KAFKA_TOPIC='filetosink4', VALUE_FORMAT='AVRO');` where `ksql_csv_issue` is the stream and `filetosink4`is the topic where we put the message from csv source connector.

### STEP4
create a new stream for cannonical model `for example: ksql_stream_project` with kafka topic `KSQL_STREAM_PROJECT` from `ksql_csv_issue` using ```CREATE STREAM ksql_stream_Project WITH (KAFKA_TOPIC='KSQL_STREAM_PROJECT', VALUE_FORMAT='AVRO') as \
SELECT PROJECTKEY,PROJECTNAME,PROJECTTYPE,PROJECTLEAD,PROJECTDESCRIPTION,PROJECTURL from ksql_csv_issue  PARTITION BY PROJECTKEY;```

### STEP5
run the kafka source and sink using ```./bin/connect-standalone ./etc/kafka/worker.properties ./etc/kafka/<csv-source-connector.properties> ./etc/kafka/<mongo-sink-connector.properties>``` the message will enter kafka `filetosink4` topic and a message with cannonical model enter into `ksql_stream_project`

we can delete an existing query using `TERMINATE <QUERY_ID>;` then `DROP STREAM <stream name>;`