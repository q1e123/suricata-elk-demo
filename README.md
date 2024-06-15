# suricata-elk-demo

This project sets up a demo environment for Suricata using Docker and the ELK stack (Elasticsearch, Logstash, Kibana). The setup helps in analyzing network traffic and visualizing the results.

## Prerequisites

- Docker
- Docker Compose

## Getting Started

### Step 1: Clone the Repository

```sh
git clone git@github.com:q1e123/suricata-elk-demo.git
cd suricata-elk-demo
```

### Step 2: Configure Suricata

Modify the `suricata/suricata.yaml` file to suit your needs. This may also include adding rules to the `suricata/rules` directory.

**You may also want to change `docker-compose.yaml` in order to sniff your intended interface.**


### Step 3: Start the Services

```sh
docker-compose up -d
```

### Step 4: Access Kibana

Open your browser and navigate to `http://localhost:5601`.

## Known issues

### vm.max_map_count

If you encounter the following error:

```
max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144]
```

You can increase the `vm.max_map_count` by running the following command:

```sh
sudo sysctl -w vm.max_map_count=262144
```