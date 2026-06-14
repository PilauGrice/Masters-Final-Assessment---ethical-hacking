---

layout: default
title: "Remediations & Source Code"
permalink: /remediations/
-------------------------

# 🔒 Vulnerable Source Code & Remediation Guidance

[⬅️ Return to Main Telemetry Dashboard](/)

---

## Vulnerable Python Service

```python
#!/usr/bin/env python3

import http.server
import urllib.parse
import os

class VulnerableCommandHandler(http.server.BaseHTTPRequestHandler):

    def do_GET(self):
        self.send_response(200)
        self.send_header("Content-type", "text/plain")
        self.end_headers()

        parsed_url = urllib.parse.urlparse(self.path)
        query = urllib.parse.parse_qs(parsed_url.query)

        if "cmd" in query:
            command_string = query["cmd"][0]
            execution_output = os.popen(command_string).read()
            self.wfile.write(execution_output.encode("utf-8"))
```

---

## Gateway Configuration

```nginx
server {
    listen 80;

    location /juiceshop/ {
        proxy_pass http://192.168.241.20:3000/;
    }

    location /dvwa/ {
        proxy_pass http://192.168.241.10:80/;
    }
}
```

---

## Security Recommendations

### Reduce Information Disclosure

```nginx
http {
    server_tokens off;
}
```

### Apply Least Privilege

```yaml
victim-ubuntu:
  user: "1001:1001"
  read_only: true

  security_opt:
    - no-new-privileges:true

  cap_drop:
    - ALL
```

### Avoid Shell Execution

Instead of executing user-supplied commands directly, restrict operations to approved functionality.

### Improve Monitoring

* Enable IDS logging
* Configure alerting
* Centralise logs
* Monitor administrative services

### Network Hardening

* Restrict inter-network communication
* Limit administrative exposure
* Enforce segmentation policies
* Apply firewall controls

---

## Summary

Recommended improvements include:

* Least privilege enforcement
* Container hardening
* Reduced attack surface
* Improved logging and monitoring
* Network segmentation controls
* Information disclosure reduction
* Secure service implementation
