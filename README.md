# helios

Scrapy spider to crawl and fetch information about real estate information

This project uses pipenv for package/dependency and virtualenv management, to learn more about how to use [pipenv](https://pipenv.readthedocs.io/en/latest/)

Requirements:

* Cassandra cluster set up

  ```bash
  docker pull cassandra
  docker run --name helios_db -d cassandra:latest
  ```

* Cassandra driver installed

  `pipenv install cassandra-driver`

  - if you don't want to have Cython-based extensions then disable through flag
  `pip install cassandra-driver --no-cython`

### Setup workspace

```bash
pipenv --two
pipeenv lock
```

### Setup Cassandra Cluster

for local dev:
```bash
# assume the following command is run from root directory
docker run --name cassandra_cluster_1 -d cassandra:3.11.3 -Dcassandra.config=./res/cassandra.yaml

docker run --name cassandra_cluster_2 -d -e CASSANDRA_SEEDS="$(docker inspect --format='{{ .NetworkSettings.IPAddress }}' cassandra_cluster_1)" cassandra:3.11.3 -Dcassandra.config=./res/cassandra.yaml

docker run --name cassandra_cluster_3 -d -e CASSANDRA_SEEDS="$(docker inspect --format='{{ .NetworkSettings.IPAddress }}' cassandra_cluster_1)" cassandra:3.11.3 -Dcassandra.config=./res/cassandra.yaml
```

[Note]
Commits are associated with GPG signing key