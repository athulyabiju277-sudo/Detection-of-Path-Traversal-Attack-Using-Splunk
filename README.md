# # Detection of Path Traversal Attack Using Splunk

##  Project Overview

This project demonstrates the detection of **Path Traversal Attacks** using **Splunk SIEM** by monitoring Apache web server logs in real time.

The project simulates malicious requests attempting to access sensitive files outside the web root directory and shows how Splunk detects suspicious patterns and triggers alerts automatically.

---

#  Aim

To monitor web server logs and detect path traversal attack attempts using Splunk SIEM.

---

#  Objective

* To add Apache web server logs into Splunk
* To identify directory traversal patterns
* To configure and trigger a Splunk alert
* To analyze suspicious requests

---

#  Tools Required

* Splunk Enterprise
* Apache Web Server Logs
* Linux / Kali Linux
* Curl Command
* Apache Access Log File

---

#  Theory

Path Traversal (Directory Traversal) is a web attack technique used by attackers to access files outside the web root directory.

Attackers use special sequences such as:

```bash id="x0d4kn"
../
..\
%2e%2e%2f
```

To access sensitive files like:

```bash id="bz0wcm"
/etc/passwd
C:\Windows\system32\drivers\etc\hosts
```

Monitoring these patterns helps detect unauthorized file access attempts.

---

#  Log Source

Apache access logs monitored:

```bash id="xkvl8f"
/var/log/apache2/access.log
```

Logs were indexed in Splunk under:

```spl id="c7g2ae"
source=*/var/log/apache2/access.log
host="ubuntu"
sourcetype="access_combined"
```

---

#  Splunk Detection Query

```spl id="5j9nrt"
index=* sourcetype=access_combined ("../" OR "..\\" OR "%2e%2e%2f")
```

---

#  Alert Configuration

Splunk alerts were configured to trigger whenever traversal attempts were detected in Apache web logs.

### Alert Features

* Real-time monitoring
* Detection of suspicious requests
* Automated alert generation

---

#  Attack Simulation

The attack was simulated using:

```bash id="s8m3vq"
curl http://<ubuntuip>/index.html?file=../../etc/passwd
```

Multiple requests were generated to simulate attacker behavior.

---

#  Results

* Splunk successfully detected suspicious requests containing path traversal patterns
* Alerts were triggered automatically
* Apache access logs were monitored in real time
* Suspicious requests were identified and analyzed

---

#  Conclusion

Splunk successfully detected path traversal attempts by monitoring Apache web server logs.

The alert mechanism enabled automated detection of suspicious requests, demonstrating how SIEM solutions help identify web attack attempts in real time.

---

#  Screenshots


* Splunk log ingestion
* Detection query
* Alert configuration
* Triggered alerts
* Attack simulation

---

#  Repository Structure

Detection-of-Path-Traversal-Attack-Using-Splunk/
│
├── README.md
├── screenshots/

```

---

#  Sample Apache Log

```log id="m9x2ca"
192.168.1.10 - - [12/May/2026:10:22:14 +0000] "GET /index.html?file=../../etc/passwd HTTP/1.1" 200 532
```

---

#  Future Improvements

* Email alert integration
* Dashboard visualization
* Detection of encoded traversal payloads
* Automated incident response
* Detection of additional web attacks

---


