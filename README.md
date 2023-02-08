# de-fullstack project
![de-fullstack architecture](./images/architecture.drawio.png?raw=true "Title")


#### Usecases
This is useful for user facing analytics that require up to date and fresh changes. Instead of batch processes at a certain time, changes can be made an reflected in almost real time including the transformations (aggregations, upserts) needed for the full analytical dataset. This allowed end users to view their data up to date all the time.
This can be useful for feature stores in machine learning teams as well.
Pinot is designed to execute OLAP queries with low latency. It is suited in contexts where fast analytics, such as aggregations, are needed on immutable data, possibly, with real-time data ingestion.

## Proposed Design:
- [Postgres database](https://www.postgresql.org/about/) to store our data.
- CDC Using [debezium](https://debezium.io/#:~:text=Debezium%20is%20an%20open%20source,apps%20commit%20to%20your%20databases.) to detect changes and [capture changes from the postgres db](https://docs.confluent.io/5.4.4/connect/debezium-connect-postgres/index.html#:~:text=The%20Debezium%20PostgreSQL%20Connector%20is,level%20changes%20to%20that%20data.).
- Apache Kafka/[Kafka Connect](https://www.baeldung.com/kafka-connectors-guide) to stream the recorded changes.
- [Apache Pinot](https://docs.pinot.apache.org/) to recieve the kafka stream with changes.
- [Superset](https://superset.apache.org/docs/intro/) to visualise these changes in real time .

Each of the above will run on Docker using docker-compose.

## Data generation
CSV and custom API developed in [de-fullstack-api](https://github.com/knvsk/de-fullstack-api)
## Data stream store
#### Apache Kafka
 - **kafka-ui**
   In order to monitor the health and status of brokers, topics and consumers `kafka-ui` is used. More [here](https://github.com/provectus/kafka-ui).
   <br>
   Screenshot:
   ![kafka-ui-example](./images/kafka-ui-vanilla.png)

## Data stream processing
#### Apache Spark

## Apache Pinot
   Screenshot:
   ![pinot-example](./images/pinot-ui-vanilla.png)


# Get started
1. Run
```
docker-compose -f docker-compose-kafka.yml -f docker-compose-pinot.yml up
```

