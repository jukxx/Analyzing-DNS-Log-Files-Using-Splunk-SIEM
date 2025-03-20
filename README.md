# Analyzing DNS Log Files Using Splunk SIEM

## Introduction
DNS logs are crucial for understanding network activity and identifying potential security threats. Splunk SIEM provides powerful capabilities for analyzing DNS logs and detecting anomalies or malicious activities.

## Uploaded Log Files to Splunk
![Screenshot 2025-03-20 114404](https://github.com/user-attachments/assets/18516bcd-74b2-45d8-9b37-ddafdc1f621a)

### Searched for DNS Events      
- Entered the following search query to retrieve DNS events   
```
index=* sourcetype=dns_sample
```
![Screenshot 2025-03-20 123722](https://github.com/user-attachments/assets/34f4b1d5-08c9-4b9d-8d32-8a6abf8f4242)

### Extracted Relevant Fields 
- Searched for common DNS-related keywords in the raw event data.
```
index=* sourcetype=dns_sample | regex _raw="(?i)\b(dns|domain|query|response|port 53)\b"
```
![Screenshot 2025-03-20 120806](https://github.com/user-attachments/assets/0d0d9657-51e5-40fe-af48-441814914169)

### Identified Anomalies
- Query to identify spikes
```
index=_* OR index=* sourcetype=dns_sample  | stats count by fqdn
```
![Screenshot 2025-03-20 120841](https://github.com/user-attachments/assets/063ba412-5159-45ee-9720-1d0d3dcca1c1)

### Looked for the top DNS sources
- Used the top command to count the occurrences of each query type:   
```
index=* sourcetype=dns_sample | top fqdn, src_ip
```
![Screenshot 2025-03-20 120946](https://github.com/user-attachments/assets/70f0175c-6a72-443f-8b54-3aa88eb9c670)


### Investigated Suspicious Domains
- Searched for domains associated with known malicious activity or suspicious behavior.
```
index=* sourcetype=dns_sample fqdn="maliciousdomain.com"
```
![Screenshot 2025-03-20 121438](https://github.com/user-attachments/assets/e18afac3-7d9c-409a-90a8-c36ef00954ab)

## Conclusion
Analyzing DNS log files using Splunk SIEM enables security professionals to detect and respond to potential security incidents effectively. By understanding DNS activity and identifying anomalies, organizations can enhance their overall security posture and protect against various cyber threats.
