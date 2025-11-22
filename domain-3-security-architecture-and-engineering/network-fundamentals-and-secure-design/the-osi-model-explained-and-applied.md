# The OSI Model Explained and Applied

The **Open Systems Interconnection (OSI) Model** is a conceptual framework that standardizes the functions of a communication system into **seven abstract layers**. While the TCP/IP model is used for actual network implementation, the OSI model remains the essential reference for diagnosing network issues, designing security controls, and understanding how threats operate.

#### Why is the OSI Model Critical for Security?

Understanding the OSI model allows a security professional to implement **Defense in Depth**. By knowing which security controls operate at which layer, you can create redundant protection and accurately identify the source of network attacks.

#### Detailed Layer Breakdown and Security Relevance

The following table details each layer, its function, typical protocols, and the associated security concerns and controls.

| Layer  | Name             | Function                                                              | Protocols/Devices                                          | Security Concerns & Controls                                                                   |
| ------ | ---------------- | --------------------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| **L7** | **Application**  | User services and applications interface with the network.            | HTTP, DNS, SMTP, FTP, Web Browsers                         | **Malware, Code Injection (XSS, SQLi)**, Input Validation, Web Application Firewalls (WAFs).   |
| **L6** | **Presentation** | Data formatting, encryption, and compression.                         | SSL/TLS (Encryption Handshake), JPEG, MPEG                 | **Improper Cryptography Use**, Secure Protocols Implementation, Data Encoding/Decoding issues. |
| **L5** | **Session**      | Establishes, manages, and terminates sessions between applications.   | NetBIOS, RPC                                               | **Session Hijacking**, Port Security, Authentication Failures.                                 |
| **L4** | **Transport**    | Segmentation, error control, and reliable/unreliable data transfer.   | **TCP** (Connection-Oriented), **UDP** (Connectionless)    | **DoS Attacks (e.g., SYN Flood)**, Port Scanning, Stateful Firewall Inspection.                |
| **L3** | **Network**      | Logical addressing and routing (path determination).                  | **IP** (IPv4/v6), ICMP, Routers                            | **IP Spoofing, Routing Table Manipulation**, Access Control Lists (ACLs) on routers.           |
| **L2** | **Data Link**    | Physical addressing (MAC), error detection, and media access control. | Ethernet, MAC Addresses, Switches                          | **ARP Poisoning, MAC Flooding**, VLAN Hopping, Port Security (802.1X).                         |
| **L1** | **Physical**     | Transmission of the raw bit stream over a physical medium.            | Cables (Fiber, Copper), Hubs, Network Interface Card (NIC) | **Physical Access Control**, Wiretapping, Eavesdropping, Signal Jamming.                       |

#### Encapsulation and Security Inspection

As data moves **down** the stack (from L7 to L1), each layer adds its own control information (headers and trailers) in a process called **encapsulation**. As data moves **up** the stack on the receiving end, the headers are stripped (**decapsulation**).
