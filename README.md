
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
