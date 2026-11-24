# Evidence index — Week 3

Open a figure to view the full-size screenshot. Lettered entries are panels of the same numbered figure.

| Figure | Screenshot | What it shows |
|---|---|---|
| 1 | [Local Suricata signatures](week3/fig-01-suricata-local-rules.png) | SID 1000001 matches an HTTP URI beginning with /admin. SID 1002101 counts TCP SYN packets to ubuntu-web by source. |
| 2 | [TCP SYN alerts in fast.log](week3/fig-02-syn-threshold-fast-log.png) | Suricata shows 10.10.10.50 reaching several ports on 10.10.10.30. The matching log count is 50. |
| 3 | [HTTP control request](week3/fig-03-normal-http-control.png) | Apache returned 200 OK for a HEAD request to /. The repeated-connection alert count was 50 before and after the check. |
| 4 | [Requests to the admin path and local alerts](week3/fig-04-admin-path-suricata.png) | Ten requests to /admin returned 404. The sensor recorded the corresponding SID 1000001 events. |
| 5 | [HTTP alerts in Wazuh](week3/fig-05-admin-path-wazuh.png) | The dashboard shows rule 100110, destination port 80 and HTTP status 404 for the ten requests. |
| 6 | [Single rejected SSH login](week3/fig-06-ssh-single-failure.png) | SSH rejected a login to the lab webadmin account. This is the individual failure used for comparison. |
| 7 | [Repeated SSH authentication test](week3/fig-07-ssh-repeat-test.png) | The test client identifies the controlled run and destination. Figure 8 shows how Wazuh classified the resulting failures. |
| 8 | [Individual and correlated Wazuh SSH alerts](week3/fig-08-ssh-failure-and-correlation.png) | Rule 5760 records authentication failures; rule 5763 identifies the repeated pattern. |
| 9 | [Native Wazuh Active Response settings](week3/fig-09-active-response-config.png) | The manager configuration ties rule 5763 to local firewall-drop execution and a 180-second timeout. |
| 10a | [Agent response log](week3/fig-10a-agent-response-log.png) | The ubuntu-web agent logged the firewall-drop exchange for 10.10.10.50 and rule 5763. |
| 10b | [Temporary firewall entry](week3/fig-10b-iptables-drop.png) | The INPUT chain on ubuntu-web contains a DROP entry for source 10.10.10.50/32. |
| 11 | [Block and automatic unblock in Wazuh](week3/fig-11-wazuh-block-unblock.png) | Rule 651 appears at 22:59:21.180; rule 652 follows at 23:02:23.741 on 17 November 2026 (dashboard time). |

The lab IPs, timestamps, rule IDs and results are retained. Figure 7 is an excerpt of test output; Figure 10a focuses on the endpoint log. Figure 10b is the firewall entry itself.
