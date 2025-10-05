# Realtime Data Streaming

This repo showcases a real-time data streaming pipeline, covering each phase from data ingestion to processing and finally storage. Utilizing Apache Airflow, Python, Apache Kafka, Apache Zookeeper, Apache Spark, and Cassandra—all neatly containerized using Docker.

## Overview

Realtime data streaming architecture built for ingesting, processing, and storing data at scale. It leverages open-source tools for orchestration, messaging, stream processing, and storage, all containerized with docker for deployment. The system is desinged to handle high-velocity data (e.g., from APIs / user interactions), processing it in real0time with Spark, and persisting it in a distirbuted database, Cassandra. Airflow orchestrates workflows, while Kafka acts as the central messaging backbone. 

1. Data Ingestion Layer

- API: Entry point for extrenal data source, in this case data comes from randomuser.me. Represents RESTful or web APIs where raw data (e.g., events, logs, or user actions) can enter the system.

- PostgreSQL: Relational database for structured, transactional data. Stores metadata, configurations, and can be used to store inintal raw data before streaming. Captures persistent records.

2. Workflow Orchestration

- Apache Airflow: Workflow management platform. Schedules, monitors, and triggers data pipelines. It receives data form the API/PostgreSQL server and feeds it inot the streaming layer, ensuring ETL (Extract-Transform-Load) jobs run reliably.

3. Messaging and Coordination

- Apache ZooKeeper: Distributed coordination service. Manages configuration, synchronization, and leader election for Kafka. Essential for kafka's high availability.

- Apache Kafka: Core event streaming platform. Acts as a durable, distributed message broker. Data from Airflow flows into Kafka topics for decoupled, real-time distribution to downstream consumers.

4. Stream Processing 

- Apache Spark Streaming: Real-time data processing engine (wiht master ndoe and multiple worker nodes). Consumes from Kafka, performs transformations (e.g., aggregations, joins, windowing), and outputs processed streams. The "Spark" labels on master/worker boxes highlight its cluster setup for scalability.

5. Data Storage

- Apache Cassandra: NoSQL distributed database. Handles high-write-throughput, time-series, or semi-strucutred data from Spark. Ideal for realtime analytics due to its linear scalabiliity and fault-tolerance. 

6. Monitoring and Management

- Control Center: Confluent Control Center. Provides a UI for monitoring Kafka clusters, topics, and consumer lag--helping ops teams visulaize pipeline health.

- Schema Registry: Mangaes Avro/Protobuf schemas for Kafka messages. Ensures data compatibility as schemas evolves, preventing breaking changes in streaming pipelines. 

7. Deployment and Infrastructure 

- Docker: All componenets are containerized. Enabling portable, scalable deployment (e.g., via kubernetes or Docker Compose).

## Real World Use Cases

- Realtime Analytics: E.g., IoT sensor data ingested via API, processed by Spark for aggregations, stored in Cassandra for databoards.

- Event-Driven Apps: User actions (API) trigger workflows (Airflow) for notifications or recommendations via Kafka/Spark.

- ETL Pipelines: Batch-to-stream hybird, with Airflow handling scheduling and kafka enabling decoupling.

architecture is:

    1. Scalable, via distributed componenets like spark workers

    2. Fault-tolerant, zookeeper for coordination

    3. schema evolution, schema registry