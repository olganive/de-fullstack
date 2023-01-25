# de-fullstack

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

## Social media post
[dev.to](https://dev.to/nvsk/data-transformations-on-streaming-data-1pae-temp-slug-2760683?preview=25f97e65807b910fa1d70ebe04c2ded8ab8a42fd7327ed4d92136d1db461236ef96cd8409334221b27dd4d84814748d6de13d25b62b9892f1310f75b)

## Resources
### Data generator
https://github.com/garystafford/streaming-sales-generator

### Change Data Analysis with Debezium and Apache Pinot
https://medium.com/apache-pinot-developer-blog/change-data-analysis-with-debezium-and-apache-pinot-b4093dc178a7

### Building a Climate Dashboard with Apache Pinot and Superset
https://medium.com/apache-pinot-developer-blog/building-a-climate-dashboard-with-apache-pinot-and-superset-d3ee8cb7941d

### Using Apache Pinot and Kafka to Analyze GitHub Events
https://medium.com/apache-pinot-developer-blog/using-apache-pinot-and-kafka-to-analyze-github-events-93cdcb57d5f7

### Spin up an Apache Pinot cluster using Docker
https://cnatsis.com/2022-07-12-pinot-cluster-docker/

### Playing PyFlink from Scratch
https://dev.to/lazypro/playing-pyflink-from-scratch-54mh

### Exploring Popular Open-source Stream Processing Technologies: Part 1 of 2
https://itnext.io/exploring-popular-open-source-stream-processing-technologies-part-1-of-2-31069337ba0e

### CDC-based Upserts with Debezium, Apache Kafka, and Apache Pinot
https://medium.com/event-driven-utopia/cdc-based-upserts-with-debezium-apache-kafka-and-apache-pinot-427cced24eb1

### Building Apache Pinot and Presto
https://dev.to/lazypro/building-apache-pinot-and-presto-4il0?signin=true

### Spin up an Apache Pinot cluster using Docker
https://cnatsis.com/2022-07-12-pinot-cluster-docker/
https://github.com/cnatsis/pinot-cluster-docker


# Apache Pinot docker-compose.yml
https://github.com/apache/pinot/blob/master/docker/images/pinot/docker-compose.yml
https://startree.ai/blog/apache-pinot-native-join-support
https://docs.pinot.apache.org/basics/getting-started/running-pinot-locally

# Flink docker-compose.yml
https://nightlies.apache.org/flink/flink-docs-master/docs/deployment/resource-providers/standalone/docker/