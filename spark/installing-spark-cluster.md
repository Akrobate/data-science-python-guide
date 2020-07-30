# Installing spark environment

## Local spark installation

Choose the installation to download: https://spark.apache.org/downloads.html

```bash
wget http://apache.crihan.fr/dist/spark/spark-3.0.0/spark-3.0.0-bin-hadoop2.7.tgz
tar -xzf spark-3.0.0-bin-hadoop2.7.tgz
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