```markdown
---
layout: default
title: "Remediations & Source Code"
permalink: /remediations/
---

# 🔒 Vulnerable Source Code & Actionable Remediation Blueprints

[⬅️ Return to Main Telemetry Dashboard](/)

---

### Vulnerable Target Daemon Source Code (`web.py`)
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
            try:
                command_string = query["cmd"][0]
                execution_output = os.popen(command_string).read()
                self.wfile.write(execution_output.encode("utf-8"))
            except Exception as e:
                self.wfile.write(f"Execution Exception Context: {str(e)}".encode("utf-8"))
        else:
            self.wfile.write(b"Custom Python Audit Daemon Status: ACTIVE. Use ?cmd= for diagnostic tracking.")

if __name__ == "__main__":
    server_address = ("", 8080)
    audit_daemon = http.server.HTTPServer(server_address, VulnerableCommandHandler)
    print("Initializing Vulnerable Target Core Service on Port 8080...")
    audit_daemon.serve_forever()

### Ingress Proxy Routing Engine Map Configuration (default.conf)
server {
    listen 80;
    server_name localhost;

    location /juiceshop/ {
        proxy_pass [http://192.168.241.20:3000/](http://192.168.241.20:3000/);
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }

    location /dvwa/ {
        proxy_pass [http://192.168.241.10:80/](http://192.168.241.10:80/);
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}


### Actionable Remediation & Hardening Blueprints

### Gateway Banner Suppression (Mitigates Finding 1 / CWE-200)

http {
    # Suppresses specific version signatures from returned headers globally
    server_tokens off;
}


### Microservice Privilege Escalation Lockdown (Mitigates Finding 3 / CWE-78)

services:
  victim-ubuntu:
    image: ubuntu:latest
    container_name: victim-ubuntu
    # Strips administrative capabilities and sets immutable file structures
    user: "1001:1001"
    read_only: true

    
