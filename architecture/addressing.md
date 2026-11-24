# Week 3 lab addressing

The tests ran on the isolated LabShop SOC-LAN (`10.10.10.0/24`) in PNETLab.

| Host | Address | Collection or response |
|---|---|---|
| Kali | 10.10.10.50 | Source of the recorded HTTP, TCP and SSH tests |
| ubuntu-web | 10.10.10.30 | Apache on TCP 80; SSH on TCP 22; Suricata on ens3; Wazuh agent 002 |
| siem-host | 10.10.10.10 | Manager, alert storage and dashboard in the single-node Wazuh deployment |

Suricata writes local alerts to `/var/log/suricata/fast.log`. Wazuh ingests the sensor’s `/var/log/suricata/eve.json`. For SSH, the agent collects authentication events independently of Suricata. The native response runs on ubuntu-web.

[Event paths](network-diagram.md)
