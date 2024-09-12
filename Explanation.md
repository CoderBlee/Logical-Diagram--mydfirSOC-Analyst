
# Cloud Security Monitoring Architecture

This repository contains a logical architecture diagram that I created for a cloud-based security monitoring setup. It shows how different components, like servers and security tools, are connected to help create an efficient Security Operations Center (SOC).

### Overview

In today’s world, securing cloud environments is super important to keep threats away and ensure everything runs smoothly. This project shows a detailed architecture for a cloud-based SOC using tools like **Elastic & Kibana**, **Fleet Server**, and **OS Ticket**. The goal is to collect logs from servers, monitor for any weird activity, and manage security incidents through alerts and tickets.

### Architecture Breakdown

#### 1. Vault (VPC)

Inside the cloud environment, there’s a **Virtual Private Cloud (VPC)**, which is a secure section of the network. I’ve set up a **private network** inside the VPC with:
- **IP range**: `172.31.0.1-254`
- **Subnet Mask**: `255.255.255.0`
- **Internet Gateway**: Allows servers in the VPC to connect to the internet.

#### 2. Servers Inside the VPC

- **Windows Server**: This server is RDP-enabled, which means we can access it remotely. It sends logs to **Elastic & Kibana** using an agent that’s managed by the **Fleet Server**.
  
- **Ubuntu Server**: This is a Linux server that we can access using SSH. It also sends logs to **Elastic & Kibana** through an agent, connected to the **Fleet Server**.

- **Fleet Server**: This is like a manager for the agents running on the other servers. It collects logs from the Windows and Ubuntu servers and sends them to the **Elastic & Kibana** server for monitoring.

- **Elastic & Kibana Server**: This is the heart of our monitoring setup. It collects all logs from the servers and shows us everything in one place, like a dashboard. It also generates alerts if it sees anything suspicious.

#### 3. Ticketing and Alerts

- **OS Ticket Server**: This server works with **Elastic & Kibana** to create tickets whenever there’s an alert. So if a security issue happens, the SOC team gets notified and can manage it through tickets.

#### 4. External Connections

- **SOC Analyst Laptop**: The analyst uses this laptop to access **Elastic & Kibana** via a web browser to view logs and alerts.
  
- **Kali Linux Attacker Machine**: This is an attacker’s laptop that’s connected to the internet, simulating real-world hacking attempts.
  
- **C2 Server (Mythic Framework)**: This is another machine connected to the internet. It represents a Command-and-Control server, which hackers might use to control their attacks.

### Network Details

- **Private Network**: `172.31.0.0/24`
- **IP Range**: `172.31.0.1-254`
- **Subnet Mask**: `255.255.255.0`
- **Internet Gateway**: Allows traffic from the VPC to the internet.

### How the System Works

1. **Log Forwarding**: 
   - Both the Windows and Ubuntu servers send their logs to the **Elastic & Kibana** server through agents.
   
2. **Fleet Server**: 
   - This server manages the connection between the servers and **Elastic & Kibana** and makes sure logs are sent correctly.

3. **Alerting**:
   - **Elastic & Kibana** sends alerts to the **OS Ticket Server**, creating a ticket for every potential security issue.

4. **SOC Monitoring**:
   - The SOC analyst uses their laptop to monitor everything in **Elastic & Kibana** through a web interface.

5. **Attacker Simulation**:
   - The **Kali Linux** attacker machine and **C2 Mythic Server** simulate external attacks. This helps test how well the system detects and responds to threats.

### How to Set It Up

Here’s how you can set up this architecture:

1. **VPC Setup**: 
   - Create a VPC in your cloud provider (like AWS) with the network settings mentioned above (IP range, subnet mask, etc.).
   
2. **Elastic & Kibana**:
   - Install the Elastic Stack (Elasticsearch and Kibana) on a server, and set up the **Fleet Server** on another machine.
   
3. **Agent Setup**:
   - Install agents on the Windows and Ubuntu servers to send logs to **Elastic & Kibana**.

4. **OS Ticket**:
   - Install OS Ticket and integrate it with Elastic & Kibana so that alerts automatically create tickets.

5. **Testing**:
   - Test if the logs are being sent from the servers to **Elastic & Kibana** and if tickets are being generated properly.

### Real-World Use Cases

Here are some situations where this architecture can be useful:

- **Monitoring Logins**: Keep track of all login attempts on the Windows and Ubuntu servers. If someone tries to break in, the system will catch it.
  
- **Detecting Failed SSH Attempts**: If someone tries and fails to log into the Ubuntu server via SSH, the system will log it and alert you.

- **Incident Management**: When there’s a security issue, a ticket is created automatically, and the SOC team can manage and resolve it.

### Security Considerations

- **Network Security**: The VPC is isolated from the public internet, which keeps it secure.
- **Firewall Rules**: Set up firewalls (security groups) to only allow the necessary traffic, like RDP for the Windows server, SSH for the Ubuntu server, and log traffic for Elastic & Kibana.
- **Encryption**: Make sure communication between the agents and Elastic & Kibana is encrypted to keep everything secure.

### Diagram

Here’s the diagram showing how everything connects. (You can include a screenshot or upload the `.drawio` file for this.)

### Future Improvements

- **Add More Tools**: You could integrate more security tools like intrusion detection systems (IDS) or machine learning-based monitoring.
- **Automation**: Set up scripts that automatically respond to incidents based on the alerts.
- **Scale It Up**: As the network grows, you can add more servers and monitoring tools.

### Conclusion

This setup shows how to build a strong cloud security monitoring system. It helps collect logs, spot threats, and manage security incidents in a clear and organized way.

