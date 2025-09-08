This project implements an open-source Network Security Monitoring (SIEM) system designed for real-time threat detection and analysis. It uses Suricata as an IDS/IPS, with the ELK Stack (Elasticsearch, Logstash, Kibana) and Filebeat for a complete log processing pipeline.

## 🚀 Key Features

- **Real-time Monitoring:** Actively monitors network traffic for threats using Suricata's powerful rule engine.
- **Centralized Logging:** Aggregates all Suricata IDS/IPS alerts into a central Elasticsearch cluster.
- **Data Enrichment:** Enriches raw logs with valuable context, including GeoIP data for source/destination IPs and custom severity tags.
- **Interactive Dashboards:** Visualizes security events and trends through custom dashboards in Kibana.
- **Scalable Architecture:** Built on a reliable and efficient architecture that can easily scale to include more log sources.

## 🏗️ System Architecture

The system is built on a decoupled architecture to ensure high performance and reliability. Filebeat acts as a lightweight agent on the network sensor, forwarding logs to a central Logstash instance for processing.

**Data Flow:**

`[Suricata Sensor]` -> `[Filebeat]` -> `[Logstash]` -> `[Elasticsearch]` -> `[Kibana]`
**Detailed Diagram:**

[Suricata Sensor Host]                         [Central ELK Server]
+-----------------+      +-----------------+      +---------------------+      +----------------+      +---------+
| Network Traffic | ---> |    Suricata     |      |                     |      |                |      |         |
|                 |      | (IDS Analysis)  |      |      Logstash       |      |  Elasticsearch |      |  Kibana |
+-----------------+      +-------+---------+      | (Ingest & Process)  | ---> | (Store & Index)| <--> | (Display |
                                 |                |                     |      |                |      | & Report)|
                                 v                +----------^----------+      +----------------+      +---------+
                         +-----------------+                 |
                         |   eve.json      |                 |
                         +-------+---------+                 |
                                 |                           |
                                 v                           |
                         +-----------------+                 |
                         |     Filebeat    | ----------------+
                         | (Read & Ship Log)|
                         +-----------------+
## 🛠️ Technology Stack

-   **Suricata:** High-performance IDS/IPS engine for network traffic analysis.
-   **Filebeat:** Lightweight log shipper for forwarding and centralizing log data.
-   **Logstash:** Centralized server for processing, parsing, and enriching data.
-   **Elasticsearch:** Distributed search and analytics engine for storing and indexing logs at scale.
-   **Kibana:** Web interface for visualizing data, creating dashboards, and exploring logs.

## ⚙️ Configuration Overview

The core logic of the system is managed by two distinct Logstash configuration files:

1.  **`logstash.yml` (Settings File):** Configures the operational environment of the Logstash service itself, defining system-level parameters like data paths, log paths, and performance settings.
2.  **`suricata.conf` (Pipeline File):** Defines the data processing logic. It contains the `input`, `filter`, and `output` stages that dictate how to receive data from Filebeat, how to enrich it (e.g., GeoIP), and where to send the final, processed event (to Elasticsearch).

This separation simplifies management and allows the system to scale gracefully.

## 🚀 Getting Started

1.  **Setup ELK Stack:** Install Elasticsearch, Logstash, and Kibana.
2.  **Setup Suricata:** Install Suricata on a network sensor and configure it to output logs to `eve.json`.
3.  **Setup Filebeat:** Install Filebeat on the Suricata host, enable the `suricata` module, and configure the output to point to your Logstash server.
4.  **Configure Logstash:** Use the provided pipeline configuration to receive and process Suricata logs.
5.  **Visualize:** Create dashboards in Kibana to monitor the `suricata-*` index.

## 🔮 Future Improvements

-   Integrate additional log sources (e.g., firewalls, web servers, Windows Event Logs).
-   Implement automated alerting for critical events using Kibana's alerting features.
-   Fine-tune Suricata rules to reduce false positives.
