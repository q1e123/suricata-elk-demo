# suricata-elk-demo

This project sets up a demo environment for Suricata using Docker and the ELK stack (Elasticsearch, Logstash, Kibana). The setup helps in analyzing network traffic and visualizing the results.

## Prerequisites

- Docker

## Getting Started

### Step 1: Clone the Repository

```sh
git clone git@github.com:q1e123/suricata-elk-demo.git
cd suricata-elk-demo
```

### Step 2: Configure Suricata

Modify the `suricata/suricata.yaml` file to suit your needs. This may also include adding rules to the `suricata/rules` directory.

**You may also want to change `docker-compose.yaml` in order to sniff your intended interface.**


#### Downloading Suricata Rules

You can download Emerging Threats Suricata rules using the following commands:

```sh
mkdir rules
curl -o rules/suricata.rules https://rules.emergingthreats.net/open/suricata/emerging.rules.tar.gz
tar -xvzf emerging.rules.tar.gz -C rules
```


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

### No alerts generated

If you don't see any alerts in Kibana, you may need to modify the `docker-compose.yaml` file to sniff the correct interface. Another issue may also be that the rules are not being loaded correctly. You can check the Suricata logs by running the following command:

```sh
docker-compose logs suricata
```

You may also create a test rule to see if Suricata is working correctly. For example, you can create a rule in the `suricata/rules` directory with the following content:

```
alert icmp any any -> any any (msg:"ICMP test"; sid:1000001;)
```