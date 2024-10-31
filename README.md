# ICS_SCADA

# ICS/SCADA - Comprehensive Study Notes

## IEC 62443 Security Levels
- **IEC 62443** is an international standard series for securing Industrial Automation and Control Systems (IACS).
- Security levels range from **SL1 to SL4**:
  - **SL1**: Basic protection against accidental violations.
  - **SL2**: Protection against intentional violations by non-skilled attackers (e.g., disgruntled employees).
  - **SL3**: Protection against deliberate attacks by skilled cybercriminals or hackers.
  - **SL4**: Advanced protection against highly sophisticated attacks, such as those by terrorists or hacktivists.

## IPsec Modes and Security
- **IPsec** provides encryption and authentication for securing IP communications.
- **Modes of IPsec**:
  - **Transport Mode**: Encrypts only the payload, leaving the original IP header intact. Suitable for secure communication within trusted networks but exposes sender/receiver details.
  - **Tunnel Mode**: Encrypts both the IP header and payload, encapsulating the entire packet with a new IP header, ensuring full protection. Commonly used for VPNs.

## NIST SP 800-53
- **NIST SP 800-53** provides guidelines on security and privacy controls for federal information systems.
- It defines **9 management control families**, including:
  - **Risk Assessment**: Identify and evaluate potential threats and vulnerabilities.
  - **Security Planning**: Develop and document security plans and policies.
  - **Program Management**: Manage implementation and responsibilities within the security program.

## ICS/SCADA Generations
1. **First Generation (Monolithic)**: Standalone, isolated systems, operating without external network connections. Low exposure to cyber threats.
2. **Second Generation (Distributed Control Systems - DCS)**: Interconnected systems for flexibility, but increased vulnerability due to network connectivity.
3. **Third Generation (Networked Systems)**: Systems connected through public or corporate networks, leading to scalability but also increased risk of cyberattacks.
4. **Fourth Generation (Internet-Enabled SCADA)**: Incorporates **IoT** and cloud services for remote access and data analytics, resulting in heightened efficiency but significant cybersecurity challenges due to public internet exposure.

## ICS/SCADA Protections - Defense in Depth (IEC 62443)
- **Defense in Depth** uses multiple layers of protection for securing IACS.
- **Six Key Steps**:
  1. **Identification and Authentication Control (IAC)**: Ensure only authorized users access the system.
  2. **Use Control (UC)**: Limit actions that authorized users can perform.
  3. **System Integrity (SI)**: Protect the system from unauthorized changes.
  4. **Data Confidentiality (DC)**: Prevent unauthorized access to data.
  5. **Restricted Data Flow (RDF)**: Control and limit the flow of information.
  6. **Timely Response to Events (TRE)**: Ensure rapid response to detected security events.
- **Availability** and **Integrity** are prioritized over **Confidentiality** in ICS/SCADA, given the critical nature of uptime and accurate operation.

## Intrusion Prevention Systems (IPS)
- **Network Intrusion Prevention Systems (NIPS)** can decrypt and monitor encrypted data if equipped with SSL/TLS decryption capabilities. This allows analysis of encrypted traffic to prevent hidden threats.

## Vulnerability Scanners
- **Vulnerability Scanners** identify weaknesses in systems but have limitations:
  - They are unable to bypass filters like firewalls and IDS/IPS.
  - They work best in local networks with fewer barriers.

## ICS Protocols and Communication
- **Modbus**: A protocol widely used in ICS. Uses **function codes** to instruct slave devices (e.g., read or write data).
- **ICMP Types**:
  1. **Echo Request (Type 8) and Echo Reply (Type 0)**:
     - **Description**: Used to check connectivity between two devices. Echo Request is the message sent, and Echo Reply is the response received, commonly used in the **ping** command.
     - **Importance**: Useful for diagnosing whether a host is active on the network and if there is connectivity between two points.
  2. **Destination Unreachable (Type 3)**:
     - **Description**: Sent when a packet cannot be delivered to its final destination. This message has subcodes indicating why the destination is unreachable, such as **Network Unreachable**, **Host Unreachable**, **Protocol Unreachable**, **Port Unreachable**, etc.
     - **Importance**: Helps understand routing issues and whether there are any restrictions or unavailability along the path to the destination.
  3. **Redirect (Type 5)**:
     - **Description**: Informs a host that there is a better route to reach the intended destination. Typically sent by a router when it detects that a host should use another router for a specific destination.
     - **Importance**: Used to improve routing efficiency in a network, but can also be a vector for attacks, such as **ICMP Redirect Attack**.
  4. **Time Exceeded (Type 11)**:
     - **Description**: Sent when the **Time to Live (TTL)** of a packet expires before reaching its destination, which may happen in cases of routing loops or if the destination is too far.
     - **Importance**: Fundamental for the **traceroute** command, which uses this message to determine the path between source and destination. Also helps identify routing loops.
  5. **Parameter Problem (Type 12)**:
     - **Description**: Sent when there is an issue with a field in the IP header, indicating that something is incorrect or missing.
     - **Importance**: Helps identify errors occurring during packet processing, especially if there is an incompatibility or error in the header structure.
  6. **Timestamp Request (Type 13) and Timestamp Reply (Type 14)**:
     - **Description**: Used to measure the time between two hosts. Timestamp Request asks for a timestamp, and Timestamp Reply provides the requested timestamp.
     - **Importance**: Though not widely used, it can be helpful for synchronization and measuring network latency.

## Netstat and Nbtstat Commands
- **netstat**: A command-line utility that displays network connections (both incoming and outgoing), routing tables, interface statistics, and more.
  - **Common Parameters**:
    - **`netstat -a`**: Displays all active connections and listening ports.
    - **`netstat -n`**: Shows active connections without resolving IP addresses to hostnames (useful for faster output).
    - **`netstat -r`**: Displays the routing table.
    - **`netstat -e`**: Shows Ethernet statistics, such as bytes sent and received.
    - **`netstat -s`**: Displays statistics for each protocol, such as TCP, UDP, ICMP.
    - **`netstat -b`**: Shows the executable involved in creating each connection or listening port.
  - **Importance**: Useful for diagnosing network issues, identifying open ports, and monitoring network traffic in real-time.

- **nbtstat**: A command-line tool used to troubleshoot NetBIOS name resolution issues.
  - **Common Parameters**:
    - **`nbtstat -a [hostname]`**: Displays the NetBIOS table of a remote computer using its hostname.
    - **`nbtstat -A [IP address]`**: Displays the NetBIOS table of a remote computer using its IP address.
    - **`nbtstat -c`**: Shows the contents of the NetBIOS name cache, including resolved names.
    - **`nbtstat -n`**: Lists local NetBIOS names registered by the computer.
    - **`nbtstat -r`**: Displays statistics of NetBIOS names resolved by broadcast and via WINS.
    - **`nbtstat -s`**: Displays the current NetBIOS sessions and their status.
  - **Importance**: Useful for diagnosing NetBIOS name resolution problems, which can impact connectivity in Windows networks.

## Information Security Model (CIA)
- **Availability**: Attacked by methods like **Denial of Service (DoS)**, which aims to make services unavailable.
- **Integrity**: Attacked by **modifications**, targeting accuracy and reliability of data (e.g., data tampering).
- **Authentication**: Attacked by **masquerade**, where an attacker impersonates legitimate users.
- **Confidentiality**: Attacked by **eavesdropping**, capturing sensitive data without authorization.

## Attacks and Exploits
- **Stuxnet**: A sophisticated malware that targeted **Siemens PLCs** to physically damage uranium centrifuges in Iran, highlighting vulnerabilities in industrial systems.
- **Zero-day**: A vulnerability exploited before the vendor is aware or a patch is available, making it highly dangerous.

## PTES (Penetration Testing Execution Standard) Phases
1. **Pre-engagement Interactions**: Establish goals, scope, and rules with the client.
2. **Intelligence Gathering**: Collect information (e.g., OSINT) on the target without direct interaction.
3. **Threat Modeling**: Identify vulnerable areas and prioritize targets based on potential threats.
4. **Vulnerability Analysis**: Identify system vulnerabilities using automated tools and manual analysis.
5. **Exploitation**: Attempt to exploit identified vulnerabilities to demonstrate their impact.
6. **Post-Exploitation**: Assess value of compromised systems, gather data, and evaluate further impact.
7. **Reporting**: Create a detailed report with vulnerabilities, exploitation steps, and remediation recommendations.

## IPsec and Network Security
- **Security Parameter Index (SPI)**: Used in IPsec to identify a specific **Security Association (SA)**, defining the security settings.
- **Authentication Header (AH)**: Ensures data integrity and authenticity but lacks **confidentiality**. Use **ESP (Encapsulating Security Payload)** for confidentiality.

## Firewalls and Network Security
- Typical **ICS/SCADA** architectures use **two firewalls**:
  1. Between the corporate network and ICS/SCADA systems.
  2. Between ICS/SCADA systems and external networks.
  - These firewalls create a **DMZ (Demilitarized Zone)** for layered protection.
- **Proxy Firewall**: Operates at the application layer, inspecting content and ensuring only legitimate communications are allowed.

## Miscellaneous Concepts
- **Network Time Protocol (NTP)**: Synchronizes system clocks, crucial for coordinated events such as authentication and logging.
- **Domain Name System (DNS)**: Translates domain names to IP addresses,
