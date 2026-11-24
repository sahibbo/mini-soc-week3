# Week 3 rules

| File | Where it belongs | Evidence |
|---|---|---|
| [suricata_local.rules](suricata_local.rules) | The two LabShop signatures in `/var/lib/suricata/rules/local.rules` on ubuntu-web. | [Figure 1](../evidence/week3/fig-01-suricata-local-rules.png) |
| [native-active-response.xml](native-active-response.xml) | A fragment of the Wazuh manager’s `ossec.conf`. The existing `firewall-drop` command has timeout support. | [Figure 9](../evidence/week3/fig-09-active-response-config.png) |

The HTTP escalation [Wazuh rule 100110](https://github.com/sahibbo/mini-soc-week2/blob/main/rules/suricata_rules.xml) was already deployed in Week 2. The Week 3 test reused it. In the Docker installation the host-side manager configuration and the effective `/var/ossec/etc/ossec.conf` were checked separately. The XML above is a section, not a complete manager configuration.
