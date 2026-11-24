# Mini-SOC in a Box — Week 3

**Blue Team Capstone | LabShop Security Operations Center**

A controlled TCP scan produced 50 Suricata threshold alerts. Ten requests to `/admin` produced ten Wazuh alerts, even though Apache returned `404` each time. A separate SSH test triggered Wazuh’s native Active Response on the web server: the source was blocked and the block was removed about three minutes later.

**Previous phase:** [Week 2 — detection engineering and endpoint monitoring](https://github.com/sahibbo/mini-soc-week2)

**Technical report:** [View PDF](docs/Week3-Technical-Report.pdf) · [Download Word](docs/Week3-Technical-Report.docx) · [Browse all 11 figures](evidence/INDEX.md)

## Lab environment

| Host | IP address | Role in these tests |
|---|---|---|
| siem-host | 10.10.10.10 | Wazuh manager and dashboard |
| ubuntu-web | 10.10.10.30 | Apache, Suricata and Wazuh agent 002 |
| Kali | 10.10.10.50 | Controlled traffic source on the isolated SOC-LAN |

## Tests and results

| Test | Observed result | Evidence |
|---|---|---|
| TCP SYN threshold | SID 1002101 tracked each source separately, with a threshold of 20 matching SYN packets in 10 seconds. The log contained 50 matching alerts. | [Rules](evidence/week3/fig-01-suricata-local-rules.png) · [fast.log](evidence/week3/fig-02-syn-threshold-fast-log.png) |
| Normal HTTP control | A single HEAD request to `/` returned 200. The scan alert count stayed at 50. | [Control](evidence/week3/fig-03-normal-http-control.png) |
| HTTP admin path | Suricata SID 1000001 matched the request URI; Wazuh rule 100110 recorded all ten events with status 404 and destination port 80. | [Sensor](evidence/week3/fig-04-admin-path-suricata.png) · [Wazuh](evidence/week3/fig-05-admin-path-wazuh.png) |
| SSH authentication | Wazuh recorded individual failures as 5760 and the repeated pattern as 5763. | [Single failure](evidence/week3/fig-06-ssh-single-failure.png) · [Correlation](evidence/week3/fig-08-ssh-failure-and-correlation.png) |
| Native Active Response | Rule 5763 invoked `firewall-drop` on the originating agent with a 180-second timeout. The endpoint had a DROP entry for 10.10.10.50/32. Wazuh recorded the block (651) and release (652). | [Configuration](evidence/week3/fig-09-active-response-config.png) · [Firewall](evidence/week3/fig-10b-iptables-drop.png) · [Timeline](evidence/week3/fig-11-wazuh-block-unblock.png) |

The scan count measures alerts, not unique ports or connections. The HTTP signature matches a URI beginning with `/admin`; an alert does not imply that the client reached an administrative page.

## Repository guide

- [Architecture and addressing](architecture/addressing.md) · [Event paths](architecture/network-diagram.md)
- [Detection rules and native response settings](rules/README.md)
- [Lab journal](journal.md)
- [Evidence index](evidence/INDEX.md)
