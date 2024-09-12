# Logical Diagram

## Cloud Security Monitoring Logical Architecture

This repository contains a logical architecture diagram illustrating a cloud-based security monitoring system. It demonstrates how various infrastructure components, including servers and security systems, are connected to form an effective Security Operations Center (SOC).

### Architecture Overview

The cloud security monitoring setup consists of a Virtual Private Cloud (VPC) inside a cloud infrastructure. Here are the key components and their interconnections:

1. **Vault**
   - The vault contains the **VPC**, which hosts a private network with CIDR block `172.31.0.0/24`, IP range `172.31.0.1-254`, and subnet mask `255.255.255.0`.
   - An **Internet Gateway** is configured within the VPC, enabling outbound traffic to the internet.

2. **Servers Inside the VPC:**
   - **Windows Server**: RDP-enabled, with an agent connection forwarding logs to the **Elastic & Kibana** server. Managed connection to the **Fleet Server**.
   - **Ubuntu Server**: SSH-enabled, forwarding logs via agent to **Elastic & Kibana**, with a managed connection to the **Fleet Server**.
   - **Fleet Server**: Acts as an intermediary, managing log forwarding and communication between the **Elastic & Kibana** server and the other servers.
   - **Elastic & Kibana Server**: Collects and visualizes logs from all systems. Connected with a managed agent to the **Fleet Server** for bi-directional communication.
   
3. **Ticketing and Alert System**
   - **OS Ticket Server**: Integrated with **Elastic & Kibana** for two-way communication, generating alerts and tickets based on monitoring data.

4. **External Connections:**
   - **SOC Analyst Laptop**: Connects to the **Elastic & Kibana** server via a web GUI for monitoring and analyzing security events.
   - **Attacker Setup**:
     - **Kali Linux Attacker Machine**: Connected to the internet, simulating external threats.
     - **C2 Server (Mythic Framework)**: Also connected to the internet, representing a Command-and-Control server for potential attacks.

### Network and Security Details

- **Private Network**: 172.31.0.0/24
  - **IP Range**: 172.31.0.1-254
  - **Subnet Mask**: 255.255.255.0
- **Internet Gateway**: Allows outbound traffic from the VPC to the internet.
  
### System Flow

1. **Log Forwarding**:
   - Logs from both the Windows (RDP) and Ubuntu (SSH) servers are forwarded to **Elastic & Kibana** using managed agents.
   
2. **Fleet Server**:
   - Manages the connection between the servers and the **Elastic & Kibana** system, ensuring bi-directional communication and log collection.

3. **Alerting**:
   - The **Elastic & Kibana** server is connected to the **OS Ticket Server** for alert and ticket generation, allowing the SOC team to address potential security incidents.
   
4. **SOC Monitoring**:
   - The SOC Analyst monitors logs and alerts through a web-based interface on the **Elastic & Kibana** server, enabling proactive security management.

5. **Attacker Simulation**:
   - **Kali Linux** and **C2 Mythic Server** represent external threats, simulating attacker behaviors to test the system's defenses and monitoring capabilities.

---

### Usage

This logical diagram is ideal for demonstrating the implementation of a cloud security monitoring solution, focusing on log collection, threat detection, and incident response workflows.


