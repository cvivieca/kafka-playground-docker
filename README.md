# Local Apache Kafka Environment with Docker Compose

This GitHub repository offers an effortlessly configurable Apache Kafka environment using Docker Compose, focused for local practice and development. It features two distinct Docker Compose configurations, each comprising Apache Kafka, Control Center, ZooKeeper, and Schema Registry components.

### Usage Instructions

#### Prerequisites

- Docker and Docker Compose installed on your local machine.
- A valid image version compatible with your system architecture (AMD64 or ARM) for Apache Kafka components.

#### Setup

1. Clone this repository to your local machine:

   ```
   git clone <repository_url>
   cd <repository_directory>
   ```

2. Customize the `.env` file:

   Edit the `.env` file to set the `HOST_IP` variable to your machine's IP address, where you intend to use the CLI. Replace `0.0.0.0` with your actual IP address.

3. Choose the Configuration

   Depending on your requirements, you can select between the single-broker setup (`docker-compose.yml`) or the multi-broker cluster setup (`docker-compose-cluster.yml`).

   - For the single-broker setup:

     ```
     docker-compose up -f docker-compose.yml
     ```

   - For the multi-broker cluster setup:

     ```
     docker-compose up -f docker-compose-cluster.yml
     ```

4. Access Components

   - Kafka: `<host_ip>:19092`
   - Control Center: `http://localhost:9021`
   - Schema Registry: `http://localhost:8081`

5. When done, shut down the environment using:

   ```
   docker-compose down
   ```

### Configuration Details

The repository includes two Docker Compose configurations:

1. **docker-compose.yml** - Single Kafka Broker Configuration
   - ZooKeeper
   - Kafka Broker (1 instance)
   - Control Center
   - Schema Registry

2. **docker-compose-cluster.yml** - Multi-Broker Kafka Cluster Configuration
   - ZooKeeper
   - Kafka Brokers (3 instances)
   - Control Center
   - Schema Registry

### Environment Customization

Copy the `.env.template` file in the repository and create a new one called `.env`. Set the following variables:

- `HOST_IP`: Replace with the IP address of your machine where you'll be using the CLI.
- `IMAGE_VERSION`: Select an appropriate image version based on your system architecture (AMD64 or ARM).

## Using the Kafka Command Line Interface (CLI)

You can interact with the Kafka environment using the Kafka command-line tools. There are two ways to access these tools: by using the CLI directly from your host machine or by accessing the Docker container running Kafka.

### Using Kafka CLI Directly

1. **Create a Topic:**
   
   Replace `HOST_IP` with your machine's IP address.
   
   ```shell
   kafka-topics --bootstrap-server HOST_IP:19092 --topic first_topic --create --partitions 3 --replication-factor 1
   ```
   
2. **Consume Messages:**
   ```shell
   kafka-console-consumer --bootstrap-server HOST_IP:19092 --topic first_topic --from-beginning
   ```

### Using Kafka CLI from Docker Container

1. **Access the Kafka Container:**

   If you're running the Kafka environment using Docker Compose, you can access the Kafka container:

   ```shell
   docker exec -it <container_name> /bin/bash
   ```

2. **Inside the Container:**
   
   Once inside the container, you can use Kafka CLI commands as usual:
   
   ```shell
   kafka-topics --bootstrap-server localhost:9092 --topic first_topic --create --partitions 3 --replication-factor 1
   ```
   
> Note that the bootstrap server address is set to `localhost:9092` because you're accessing Kafka from within the container.

Remember to adjust the IP address and other parameters as needed for your specific use case. Experiment with Kafka CLI commands to explore its capabilities within your Dockerized Kafka environment.
