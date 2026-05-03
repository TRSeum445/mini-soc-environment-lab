# Mini SOC Environment Lab

## Overview

This project is a practical Mini Security Operations Centre (SOC) lab built in a controlled virtual environment. The lab demonstrates network segmentation, firewall rule management, routing, NAT, web server deployment, log analysis, and packet-level traffic investigation.

The environment was designed using three virtual machines: an internal workstation, a gateway firewall, and a DMZ web server. The main goal was to understand how traffic moves between network zones, how firewall rules control access, and how insecure web communication can be detected using logs and packet captures.

This project was completed in a private virtual lab environment for educational and ethical cybersecurity practice.

## Lab Environment

- Gateway Server: Ubuntu Server
- Internal Workstation: Kali Linux
- DMZ Web Server: Ubuntu Server with Apache
- Virtualisation Platform: VirtualBox
- Network Zones: Internal Network, Gateway, DMZ, Internet/NAT
- Main Tools Used: iptables, Netplan, Apache, Wireshark, Linux logs

## Project Architecture

The lab was designed using a segmented network model:

```text
Internal Network  --->  Gateway Firewall  --->  DMZ Web Server
                          |
                          ---> Internet/NAT
```

The gateway server was configured as the central control point between the internal network, the DMZ, and the internet. It handled routing, NAT, firewall filtering, and logging.

## Skills Demonstrated

- Network segmentation
- Linux server configuration
- Static IP addressing with Netplan
- Routing and NAT configuration
- iptables firewall rule management
- Default-deny firewall policy design
- Firewall logging using a custom LOG_DROP chain
- Apache web server deployment
- Web server access log analysis
- Wireshark packet capture and filtering
- HTTP GET and POST traffic analysis
- Identification of plaintext credential exposure
- SOC-style investigation and documentation
- Security recommendation writing

## Project Sections

### 1. Network Setup and Routing

In this section, I created the base network environment using VirtualBox. The gateway server was configured with multiple network interfaces to connect the internal network, DMZ, and internet/NAT network.

Static IP addresses were assigned to each zone, and IP forwarding was enabled so the gateway could route traffic between networks. NAT was configured to allow the internal workstation to reach external networks through the gateway.

### 2. Firewall Analysis

In this section, I configured the gateway firewall using iptables. I first created a default-deny style setup by using a custom LOG_DROP chain to log and drop unwanted forwarded traffic.

Then I added rules step by step to allow only required traffic, including ICMP, DNS, HTTP, and HTTPS. This showed how firewall rules can control traffic flow and support SOC-style visibility through logging.

### 3. Web Server Deployment and Traffic Investigation

In this section, I deployed an Apache web server in the DMZ and allowed controlled access from the internal workstation. The web server hosted basic login pages to generate HTTP traffic for analysis.

Apache access logs were reviewed to understand how GET and POST requests appear at the application layer. Wireshark was then used to inspect HTTP traffic and identify how credentials can be exposed when transmitted over unencrypted HTTP.

## Key Findings

The lab showed that network segmentation helps separate systems into different security zones and reduces direct exposure between internal and public-facing systems.

Firewall rules are important for controlling which traffic is allowed between zones. A default-deny approach provides stronger control because only required traffic is permitted.

The traffic analysis showed that HTTP is not safe for login forms because credentials can be captured in plaintext. GET requests expose credentials in the URL, while POST requests hide them from the URL but still send them in plaintext if HTTPS is not used.

## Security Recommendations

- Use HTTPS for all login pages and sensitive web traffic.
- Apply a default-deny firewall policy and only allow required ports and protocols.
- Restrict unnecessary outbound traffic from the DMZ.
- Enable centralised logging and monitoring for firewall, web server, and system logs.
- Keep servers updated with regular patching and hardening.
- Use strong authentication and restrict administrative access.
- Consider brute-force protection using tools such as Fail2Ban or web application security controls.
- Monitor network traffic for suspicious patterns and plaintext credential exposure.

## Ethical Notice

This project was completed only in a private virtual lab environment. The techniques and tools used in this project are intended for learning, security analysis, and ethical cybersecurity practice only.

## Report

The full project report is available in this repository as:

```text
Mini_SOC_Environment_Personal_Project.pdf
```
