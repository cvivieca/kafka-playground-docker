# Local Apache Kafka Environment with Docker Compose

This GitHub repository offers an effortlessly configurable Apache Kafka environment using Docker Compose, tailored for local practice and development. It features two distinct Docker Compose configurations, each comprising Apache Kafka, Control Center, ZooKeeper, and Schema Registry components.

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

   - Kafka: `PLAINTEXT://<host_ip>:9093`
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

**Note:** This repository is for educational and practice purposes. It's not intended for production use. Make sure to check the official documentation for advanced configurations and security considerations.
