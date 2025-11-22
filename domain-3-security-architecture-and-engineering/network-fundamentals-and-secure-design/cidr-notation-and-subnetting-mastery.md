# CIDR Notation and Subnetting Mastery

#### From Classful to Classless

**The CIDR Solution**

**CIDR (Classless Inter-Domain Routing)** is the current standard for addressing on the Internet. It was introduced to replace the inefficient **Classful Addressing** system (Classes A, B, and C), which led to rapid exhaustion of the IPv4 address space.

CIDR allows for the flexible allocation of IP addresses, enabling:

1. **Route Aggregation (Supernetting):** Combining multiple smaller networks into one larger routing entry.
2. **Efficient Subnetting:** Creating subnets of any size, not just those dictated by the old A, B, or C boundaries.

**The Notation**

The CIDR format is simple and universal:

$$
\text{IP Address}/\text{Prefix Length}
$$

* **IP Address:** The network address (e.g., `192.168.1.0`).
* **Prefix Length:** The number of bits used to identify the **Network ID**. This is the number that follows the slash (e.g., `/24`).

#### Subnetting and the Math of CIDR

In an IPv4 address (32 bits), the prefix length determines how many bits are for the **Network ID** and how many are for the **Host ID**.

$$
\text{Network Bits} + \text{Host Bits} = 32
$$

**Translating the Prefix Length**

The prefix length (`/x`) is a direct shorthand for the subnet mask. The following table provides the lookup necessary to convert the dotted-decimal subnet mask value into its corresponding prefix length.

| Decimal (x) | x.0.0.0 | 255.x.0.0 | 255.255.x.0 | 255.255.255.0 |
| ----------- | ------- | --------- | ----------- | ------------- |
| **128**     | `/1`    | `/9`      | `/17`       | `/25`         |
| **192**     | `/2`    | `/10`     | `/18`       | `/26`         |
| **224**     | `/3`    | `/11`     | `/19`       | `/27`         |
| **240**     | `/4`    | `/12`     | `/20`       | `/28`         |
| **248**     | `/5`    | `/13`     | `/21`       | `/29`         |
| **252**     | `/6`    | `/14`     | `/22`       | `/30`         |
| **254**     | `/7`    | `/15`     | `/23`       | `/31`         |
| **255**     | `/8`    | `/16`     | `/24`       | `/32`         |

{% hint style="info" %}
A subnet mask of `255.224.0.0` is `11111111.11100000.00000000.00000000` in binary, or **11 ones**, hence `/11`.
{% endhint %}

**Calculating Host and Subnet Space**

When subnetting, you "borrow" bits from the Host ID to extend the Network ID.

* **Number of Usable Hosts:** If `h` is the number of host bits (the remaining unmasked bits), the number of usable addresses, minus 2 for the Network ID and the Broadcast Address, is:

$$
2^h-2
$$

* **Number of Subnets Created:** If `s` is the number of bits borrowed, the number of new subnets created is:

$$
2^s
$$

#### Security Implications of CIDR

CIDR is a powerful tool for r**educing the attack surface** and implementing the **Principle of Least Privilege** at the network layer.

* **Network Segmentation:** Subnetting is the foundation of network segmentation. By creating distinct, small subnets (like a DMZ, a Database subnet, or a Management subnet), you can **isolate** high-value assets and prevent an attacker who compromises one subnet from easily accessing another.
* **Firewall Rules and ACLs:** CIDR makes firewall and router Access Control List (ACL) configuration efficient:
  * Instead of writing a rule for every single IP address in a range, security professionals use a single CIDR block (e.g., to block all traffic from the `10.10.0.0/16` block).
  * This reduces complexity and the chance of misconfiguration.
* **Route Aggregation:** While primarily an efficiency gain for routing, reducing the number of advertised routes to the external network minimizes the information an external attacker can gather about the internal network structure.
