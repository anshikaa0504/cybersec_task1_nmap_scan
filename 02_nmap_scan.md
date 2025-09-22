```markdown
Date (IST): 2025-09-22
Network Range Scanned: 192.168.1.0/24
Scan Type: TCP SYN Scan (-sS)
Tool: Nmap 7.98

--- Scan Results ---
Host: 192.168.1.1
Open Ports: 23/tcp (telnet - filtered), 53/tcp (domain), 80/tcp (http), 443/tcp (https)
MAC Address: XX:XX:XX:XX:XX:XX

Host: 192.168.1.54
Open Ports: None (all scanned ports closed)
MAC Address: XX:XX:XX:XX:XX:XX

Host: 192.168.1.75
Open Ports: 8008/tcp (http), 8009/tcp (ajp13), 8443/tcp (https-alt), 9000/tcp (cslistener)
MAC Address: XX:XX:XX:XX:XX:XX

Host: 192.168.1.240
Open Ports: 80/tcp (http), 554/tcp (rtsp)
MAC Address: XX:XX:XX:XX:XX:XX

Host: 192.168.1.126 (my machine)
Open Ports: 135/tcp (msrpc), 139/tcp (netbios-ssn), 445/tcp (microsoft-ds), 5357/tcp (wsdapi)


--- Analysis of Open Ports ---

- **192.168.1.1**: Telnet (23) is filtered but insecure; DNS (53) and HTTP (80) may leak information.
- **192.168.1.54**: No open ports — low risk.
- **192.168.1.75**: Multiple services (8008, 8009, 8443, 9000) — check authentication and security settings.
- **192.168.1.240**: HTTP (80) and RTSP (554) — RTSP might expose media streams if not secured.
- **192.168.1.126 (my machine)**: Windows services (135, 139, 445, 5357) — could be targeted; ensure firewall is enabled.


## Step 6: Services Research

| Service      | Description |
|-------------|-------------|
| http (80/tcp) | Web server, unencrypted web traffic. |
| https (443/tcp) | Web server with TLS/SSL encryption. |
| msrpc (135/tcp) | Windows Remote Procedure Call; used for inter-process communication. |
| netbios-ssn (139/tcp) | Windows file and printer sharing. |
| microsoft-ds (445/tcp) | SMB/CIFS file sharing. |
| wsdapi (5357/tcp) | Web Services for Devices; allows network discovery of devices. |
| telnet (23/tcp) | Remote terminal access; plaintext passwords. |
| domain (53/tcp) | DNS service for resolving hostnames. |
| ospf-lite (8899/tcp) | Routing protocol service for network devices. |
| iphone-sync (62078/tcp) | Apple device sync service. |
| ajp13 (8009/tcp) | Tomcat server connector (AJP). |
| cslistener (9000/tcp) | Application listener service. |
| rtsp (554/tcp) | Real-Time Streaming Protocol; used for video/audio streams. |
| unknown (49152/tcp) | Unknown service; could be custom app or dynamic port. |

## Step 7: Potential Security Risks

| Host           | Port      | Service      | Potential Risk |
|----------------|----------|-------------|----------------|
| 192.168.1.1    | 23/tcp   | telnet      | Passwords can be intercepted; unauthorized access. |
| 192.168.1.1    | 53/tcp   | domain      | DNS spoofing or cache poisoning. |
| 192.168.1.1    | 80/tcp   | http        | MITM attacks; sensitive data exposure. |
| 192.168.1.1    | 443/tcp  | https       | Misconfigured SSL can allow attacks. |
| 192.168.1.126  | 135/tcp  | msrpc       | Exploitable via malware/ransomware. |
| 192.168.1.126  | 139/tcp  | netbios-ssn | SMB vulnerabilities; lateral movement possible. |
| 192.168.1.126  | 445/tcp  | microsoft-ds | Ransomware and malware propagation. |
| 192.168.1.126  | 5357/tcp | wsdapi      | Device info leakage; unauthorized access. |
| 192.168.1.135  | 80/tcp   | http        | MITM, sensitive data exposure. |
| 192.168.1.135  | 8899/tcp | ospf-lite   | Possible network mapping or DoS attacks. |
| 192.168.1.139  | 49152/tcp| unknown     | Unknown vulnerabilities; potential exploits. |
| 192.168.1.139  | 62078/tcp| iphone-sync | Device data exposure if untrusted connections. |
| 192.168.1.140  | 8008/tcp | http        | Same as HTTP. |
| 192.168.1.140  | 8009/tcp | ajp13       | Remote code execution possible if exposed. |
| 192.168.1.140  | 8443/tcp | https-alt   | Misconfigured SSL/TLS. |
| 192.168.1.140  | 9000/tcp | cslistener  | Possible unauthorized access. |
| 192.168.1.240  | 80/tcp   | http        | MITM, sensitive data exposure. |
| 192.168.1.240  | 554/tcp  | rtsp        | Video stream interception or unauthorized access. |


--- END ---
```
