# Optix connection to InfluxDB database

This sample project shows how to connect to InfluxDB instances (both embedded and self-hosted) using FactoryTalk Optix IDE.

## Setup procedure

### 1. Setup of the InfluxDB instance

1. On a device with Docker and the composer plugin installed, create the following `docker-compose.yml` file:

```yaml
services:
  influxdb:
    image: influxdb:latest
    container_name: influxdb
    ports:
      - '8086:8086'
    volumes:
      - influxdb-storage:/var/lib/influxdb2
    restart: unless-stopped
    environment:
      - DOCKER_INFLUXDB_INIT_MODE=setup
      - DOCKER_INFLUXDB_INIT_USERNAME=admin
      - DOCKER_INFLUXDB_INIT_PASSWORD=admin_pass
      - DOCKER_INFLUXDB_INIT_ORG=organization
      - DOCKER_INFLUXDB_INIT_BUCKET=bucket
      - DOCKER_INFLUXDB_INIT_RETENTION=4w
      - DOCKER_INFLUXDB_INIT_ADMIN_TOKEN=MyVeryLongAndS3cr3tTok3nToWriteD4t4

volumes:
  influxdb-storage:
```

2. Start the container using `docker compose up -d`.

### 2. Setup of the Optix project

1. Navigate to `Optix_Sample_InfluxDB/DataStores/RemoteInfluxDBDatabase1/Server` and set the IP address of the machine where the InfluxDB instance is running.

### 3. Execution of the Optix project

Start the Optix project and observe the data being written to the InfluxDB instances. The first tab of the MainWindow shows the local InfluxDB instance (running inside FactoryTalk Optix IDE), while the second tab shows the remote InfluxDB instance (running on the machine where the Docker container is running).

## Disclaimer

Rockwell Automation maintains these repositories for your convenience and that of other users. Although Rockwell Automation has the right at any time and for any reason to not access, edit, or remove content from this Repository, you acknowledge and agree to accept sole responsibility and liability for any Repository content posted, transmitted, downloaded, or used by you. Rockwell Automation has no obligation to monitor or update Repository content

The examples provided are to be used as a reference for building your own application and should not be used in production as-is. It is recommended to adapt the example for the purpose and observe the highest safety standards.