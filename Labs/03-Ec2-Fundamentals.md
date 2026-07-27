# Lab 03 — EC2 Fundamentals

## What I built
Launched a t2.micro (Amazon Linux 2023) in us-east-1 with user data
that installs Apache on boot and serves a page. Configured a security
group for SSH + HTTP, then tested reachability by breaking and fixing
the HTTP rule.

## User data script
````bash
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>Hello from $(hostname -f)</h1>" > /var/www/html/index.html
````

## What I tested
- Pasted the instance's public IP into a browser → saw the "Hello" page.
  Confirms user data ran at boot and the HTTP rule works.
- Removed the HTTP (port 80) inbound rule → page stopped loading.
- Added the rule back → page returned.

## Takeaway
Security groups control what can reach an instance. User data runs once
at launch to bootstrap the instance. No HTTP rule = no web traffic,
even though the server is running fine.

## Core Four — IAM rebuild (from memory)
- Rep 1 (Jul 25): 2:01.41
- Rep 2 (Jul 26): 1:03.80

<img width="961" height="1051" alt="aws03" src="https://github.com/user-attachments/assets/04cc4249-1049-45a3-a7a9-bd19f654fe24" />
