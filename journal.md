# Week 3 lab journal

**17 November 2026 · LabShop SOC-LAN**

1. **Detect a burst of TCP connections.** The local Suricata rules retained the Week 2 HTTP signature and added SID 1002101 for SYN packets. After the controlled scan, the log contained 50 matches; a normal HTTP HEAD request returned 200 and left that count unchanged. [Figures 1–3](evidence/INDEX.md)
2. **Trace an HTTP request into Wazuh.** Ten requests for `/admin` returned 404. Suricata logged the URI match, and the manager showed ten 100110 alerts with destination port 80. [Figures 4–5](evidence/INDEX.md)
3. **Distinguish one login failure from a pattern.** One test login was rejected. During the repeated test, Wazuh reported individual failures (5760) and SSH brute-force correlation (5763). [Figures 6–8](evidence/INDEX.md)
4. **Verify the effective response configuration.** The host-side manager file contained the new response stanza, but the active container file initially lacked it. The files were synchronized and the manager services checked after restart. The stanza selected `local` and a timeout of 180 seconds. [Figure 9](evidence/week3/fig-09-active-response-config.png)
5. **Verify enforcement and release.** The ubuntu-web agent recorded the response and its INPUT chain contained the source DROP. Rule 651 was visible at 22:59:21.180 and rule 652 at 23:02:23.741 (dashboard time). These are event timestamps; the configured timeout was 180 seconds. [Figures 10–11](evidence/INDEX.md)
