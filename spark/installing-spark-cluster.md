# Installing spark environment

- [Installing spark environment](#installing-spark-environment)
  * [Local spark installation](#local-spark-installation)
  * [Python libraries to work with spark cluster](#python-libraries-to-work-with-spark-cluster)
    + [Install with conda](#install-with-conda)
    + [Install with pip](#install-with-pip)
  * [Docker-compose](#docker-compose)
  * [Stand alone docker](#stand-alone-docker)
    + [Env configuration for stand alone docker](#env-configuration-for-stand-alone-docker)
    + [Command to launch](#command-to-launch)

## Local spark installation

Choose the installation to download: https://spark.apache.org/downloads.html

```bash
# Install JAVA
sudo apt install openjdk-8-jre

# Download spark
wget http://apache.crihan.fr/dist/spark/spark-3.0.0/spark-3.0.0-bin-hadoop2.7.tgz

# Decompress spark
tar -xf spark-3.0.0-bin-hadoop2.7.tgz
cd spark-3.0.0-bin-hadoop2.7/
```

```bash
# start spark console
./bin/pyspark --master spark://IP:PORT
```

## Python libraries to work with spark cluster

### Install with conda

```bash
conda install -c conda-forge pyspark
conda install -c conda-forge findspark
```

If conda installation is problematic use pip instead

### Install with pip

```bash
pip install pyspark
pip install findspark
```

## Docker-compose

```yaml
version: '2'

services:
  spark:
    image: docker.io/bitnami/spark:3-debian-10
    environment:
      - SPARK_MODE=master
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
    ports:
      - '8080:8080'
      - '7077:7077'
  spark-worker-1:
    image: docker.io/bitnami/spark:3-debian-10
    environment:
      - SPARK_MODE=worker
      - SPARK_MASTER_URL=spark://spark:7077
      - SPARK_WORKER_MEMORY=1G
      - SPARK_WORKER_CORES=1
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
  spark-worker-2:
    image: docker.io/bitnami/spark:3-debian-10
    environment:
      - SPARK_MODE=worker
      - SPARK_MASTER_URL=spark://spark:7077
      - SPARK_WORKER_MEMORY=1G
      - SPARK_WORKER_CORES=1
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
```

## Stand alone docker

### Env configuration for stand alone docker

File: **env.list**
```ini
SPARK_MODE=worker
SPARK_MASTER_URL=spark://192.168.1.47:7077
SPARK_WORKER_MEMORY=1G
SPARK_WORKER_CORES=1
SPARK_RPC_AUTHENTICATION_ENABLED=no
SPARK_RPC_ENCRYPTION_ENABLED=no
SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
SPARK_SSL_ENABLED=no
```

### Command to launch
```sh
docker run bitnami/spark:3-debian-10 --env-file env.list
```