# Network and SSH event paths

```mermaid
flowchart TD
    K["Kali · 10.10.10.50"] -->|HTTP and TCP| S["Suricata on ubuntu-web"]
    K -->|SSH authentication| H["sshd on ubuntu-web"]
    S -->|EVE JSON| A["Wazuh agent 002"]
    H -->|Authentication events| A
    A --> M["Wazuh manager"]
    M -->|Rule 5763| F["firewall-drop on ubuntu-web"]
    F -->|Block and unblock records| M
```

The sensor’s local TCP alerts and the manager’s HTTP and SSH alerts have different identifiers. The numbers are mapped in the [test results](../README.md#tests-and-results).
