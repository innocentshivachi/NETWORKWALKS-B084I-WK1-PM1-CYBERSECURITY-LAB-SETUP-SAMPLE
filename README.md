  # 🔐 Cybersecurity Lab Environment Setup

  **Building a Virtual Cybersecurity Lab Using VirtualBox and Kali Linux**

---

## 📌 Project Overview

This project focuses on setting up a virtual cybersecurity laboratory using Oracle VirtualBox and Kali Linux.

The purpose of this project is to establish a controlled environment for learning networking, cybersecurity fundamentals, network reconnaissance, vulnerability assessment, and penetration testing.

The lab uses a VirtualBox NAT Network with the IPv4 subnet `10.0.0.0/24`. This network is intended to support communication between multiple virtual machines while allowing internet access.

The laboratory can be expanded in the future by adding a Windows virtual machine to practice defensive security, network monitoring, and authorized security testing.

---

## 🎯 Project Objectives

The main objectives of this project are to:

* Install and configure Oracle VirtualBox.
* Set up Kali Linux as a cybersecurity testing machine.
* Create a VirtualBox NAT Network.
* Configure the virtual network to use `10.0.0.0/24`.
* Connect Kali Linux to the configured NAT Network.
* Verify the IP address and network interface configuration.
* Test connectivity between the virtual machine and its gateway.
* Verify internet connectivity and DNS resolution.
* Document the laboratory setup using screenshots.
* Prepare the environment for future cybersecurity projects.

---

## 🛡️ Purpose of the Lab

This laboratory provides an environment for practical cybersecurity learning.

It can be used for:

* Network reconnaissance.
* Port scanning.
* Network troubleshooting.
* DNS resolution testing.
* Vulnerability assessment.
* Web application security testing.
* Linux administration.
* Security tool experimentation.
* Communication testing between virtual machines.
* Defensive security and monitoring exercises.

**Ethical Use:** All security testing must be conducted on systems you own or have explicit permission to test.

---

## 🏗️ Lab Architecture

The laboratory is designed around the following components:

| Component       | Purpose                                                                 |
| --------------- | ----------------------------------------------------------------------- |
| Host Machine    | Runs VirtualBox                                                         |
| VirtualBox      | Provides virtualization                                                 |
| Kali Linux VM   | Cybersecurity testing machine                                           |
| NAT Network     | Enables communication between connected VMs and outbound network access |
| Windows VM      | Planned additional machine for testing and defensive security           |
| Virtual Network | `10.0.0.0/24`                                                           |

### Planned Network Layout

```text
                  INTERNET
                      |
                VirtualBox NAT
                      |
             NAT Network: 10.0.0.0/24
                      |
             +--------+--------+
             |                 |
        Kali Linux VM      Windows VM
        Testing Machine    Planned Target
```

*Note: The Windows VM is shown as a planned component. Update this diagram after the machine has been configured and connected successfully.*

---

## ⚙️ Lab Configuration

The following table describes the intended laboratory configuration.

| Component                  | Configuration                              |
| -------------------------- | ------------------------------------------ |
| Host Operating System      | Windows                                    |
| Virtualization Software    | Oracle VirtualBox                          |
| Attacking/Testing Machine  | Kali Linux                                 |
| Virtual Network Mode       | NAT Network                                |
| Network Address            | `10.0.0.0/24`                              |
| Subnet Mask                | `255.255.255.0`                            |
| Network Gateway            | Verify from the actual configuration       |
| Kali Linux IP Address      | Verify after connecting to the NAT Network |
| DNS Server                 | Verify from the actual configuration       |
| Additional Virtual Machine | Windows 10, planned                        |
| Network Verification Tools | `ip`, `ping`, `ip route`, `nslookup`       |

**Important:** The IP address, gateway, and DNS server should be updated to match the actual output from your virtual machine. Do not assume that the values are correct until you have verified them.

---

# 🪜 Lab Setup Procedure

## Step 1: Install VirtualBox

Oracle VirtualBox is used to create and manage the virtual machines.

The application allows Kali Linux and other operating systems to run in isolated virtual environments on the host computer.

Official download:

[Oracle VirtualBox Downloads](https://www.virtualbox.org/wiki/Downloads)

### Verification

Open VirtualBox and confirm that your Kali Linux virtual machine is listed.

**Screenshot:** `screenshots/01-virtualbox-home.png`

---

## Step 2: Set Up Kali Linux

Kali Linux is used as the cybersecurity testing machine.

The virtual machine provides access to Linux command-line tools and cybersecurity utilities used for learning and authorized security testing.

Official download:

[Kali Linux Downloads](https://www.kali.org/get-kali/)

### Configuration

1. Open VirtualBox.
2. Select the Kali Linux virtual machine.
3. Open the virtual machine's settings.
4. Navigate to Network.
5. Configure Adapter 1 to use the NAT Network created for this project.
6. Save the configuration.
7. Start Kali Linux.

**Screenshot:** `screenshots/02-kali-linux-running.png`

---

## Step 3: Create a NAT Network

A NAT Network is configured in VirtualBox to provide a shared virtual network for the laboratory.

### Configuration

The intended network settings are:

| Setting      | Value                                       |
| ------------ | ------------------------------------------- |
| Network Name | `NatNetwork`                                |
| IPv4 Network | `10.0.0.0/24`                               |
| DHCP         | Enable if required                          |
| IPv6         | Configure according to the lab requirements |

### Procedure

1. Open VirtualBox.
2. Open the Network settings.
3. Locate the NAT Networks section.
4. Create a new NAT Network if one does not already exist.
5. Set the IPv4 prefix to `10.0.0.0/24`.
6. Configure DHCP according to the project requirements.
7. Save the settings.

**Screenshot:** `screenshots/03-nat-network-configuration.png`

---

## Step 4: Connect Kali Linux to the NAT Network

After creating the NAT Network, connect the Kali Linux virtual machine to it.

### Procedure

1. Shut down Kali Linux if it is running.
2. Open the virtual machine's settings in VirtualBox.
3. Select Network.
4. Enable Adapter 1.
5. Select `NAT Network` as the attachment type.
6. Choose the configured network, such as `NatNetwork`.
7. Save the settings.
8. Start Kali Linux.

The exact network name should match the NAT Network created in VirtualBox.

**Screenshot:** `screenshots/04-kali-network-settings.png`

---

## Step 5: Verify the Network Configuration

Once Kali Linux starts, open the terminal.

### Check Network Interfaces

Run:

```bash
ip a
```

This command displays the network interfaces and their IP addresses.

Identify the interface connected to the VirtualBox NAT Network.

### Check the Routing Table

Run:

```bash
ip route
```

This displays the routing table, including the default gateway when one is configured.

### Check DNS Configuration

Run:

```bash
cat /etc/resolv.conf
```

This displays the DNS resolver configuration currently available to the system.

Record the actual values returned by these commands.

**Screenshot:** `screenshots/05-kali-ip-configuration.png`

---

## Step 6: Test Network Connectivity

Network connectivity should be tested before proceeding with additional cybersecurity exercises.

### Test the Default Gateway

First, identify the default gateway using:

```bash
ip route
```

Then test the gateway address shown in the output.

Example:

```bash
ping -c 4 10.0.0.1
```

*Replace `10.0.0.1` with the actual gateway address if it differs.*

Successful replies indicate that the gateway is reachable.

### Test Internet Connectivity

Run:

```bash
ping -c 4 8.8.8.8
```

This tests connectivity to Google's public DNS IP address.

A successful response indicates IP connectivity to that destination.

### Test DNS Resolution

Run:

```bash
nslookup google.com
```

This checks whether the configured DNS resolver can resolve the domain name.

### Expected Results

| Test                  | Command                  | Expected Result                                               |
| --------------------- | ------------------------ | ------------------------------------------------------------- |
| Network interfaces    | `ip a`                   | Network interfaces and assigned addresses are displayed       |
| Routing table         | `ip route`               | Routes and the default gateway are displayed when configured  |
| Gateway connectivity  | `ping -c 4 <gateway-IP>` | Replies if the gateway is reachable and ICMP is permitted     |
| Internet connectivity | `ping -c 4 8.8.8.8`      | Replies if the destination is reachable and ICMP is permitted |
| DNS resolution        | `nslookup google.com`    | The domain resolves to one or more IP addresses               |

*Note: A failed ping does not always mean that a network is disconnected. ICMP traffic may be filtered. Investigate the routing table, DNS configuration, and other connectivity tests before concluding that the network is unavailable.*

**Screenshot:** `screenshots/06-network-connectivity-tests.png`

---

## Step 7: Verify Cybersecurity Tools

Kali Linux includes several tools useful for cybersecurity learning.

To verify that Nmap is available, run:

```bash
nmap --version
```

This displays the installed Nmap version.

Nmap can later be used to discover hosts and identify open ports on systems within the authorized laboratory.

**Screenshot:** `screenshots/07-nmap-version.png`

---

## 📸 Project Screenshots

Screenshots provide evidence that the laboratory was configured and tested.

Create a folder named `screenshots` in the repository and add your actual screenshots.

Suggested structure:

```text
CYBERSECURITY-LAB-SETUP/
│
├── README.md
│
└── screenshots/
    ├── 01-virtualbox-home.png
    ├── 02-kali-linux-running.png
    ├── 03-nat-network-configuration.png
    ├── 04-kali-network-settings.png
    ├── 05-kali-ip-configuration.png
    ├── 06-network-connectivity-tests.png
    └── 07-nmap-version.png
```

Use the actual screenshots from your setup. Do not add placeholder images or screenshots from another person's repository as proof of your own work.

---

## 🐞 Problems Encountered and Troubleshooting

Document any problems encountered during the setup and explain how they were resolved.

### Problem 1: Kali Linux Has No Internet Connection

**Possible causes:**

* The virtual machine is connected to the wrong network.
* The NAT Network is disabled or incorrectly configured.
* The virtual machine has no valid IP address.
* The default gateway or DNS resolver is incorrectly configured.

**Troubleshooting commands:**

```bash
ip a
```

```bash
ip route
```

```bash
cat /etc/resolv.conf
```

These commands help identify whether the problem involves IP addressing, routing, or DNS.

### Problem 2: DNS Resolution Fails

If a domain name cannot be resolved, test IP connectivity first:

```bash
ping -c 4 8.8.8.8
```

Then test DNS resolution:

```bash
nslookup google.com
```

If IP connectivity works but DNS resolution fails, investigate the DNS configuration.

### Problem 3: Kali Linux Does Not Receive an IP Address

Check whether the virtual network adapter is enabled and connected to the correct NAT Network.

Run:

```bash
ip a
```

Check the DHCP configuration in VirtualBox if DHCP is being used.

Record the actual error message and the steps taken to resolve it.

*Only list problems you actually encountered, and update this section with your own findings.*

---

## 💡 What I Learned

This project provides practical experience in configuring a virtual cybersecurity environment.

The main learning areas include:

### 1. Virtualization

Understanding how VirtualBox allows multiple operating systems to run on one physical computer.

### 2. Virtual Networking

Learning how virtual network adapters connect virtual machines to different network configurations.

### 3. IP Addressing and Subnetting

Understanding IPv4 addresses, subnet masks, network prefixes, gateways, and how devices communicate within a subnet.

### 4. NAT Network

Learning how a VirtualBox NAT Network allows connected virtual machines to communicate with each other while supporting outbound network connectivity.

### 5. Linux Network Troubleshooting

Using commands such as `ip a`, `ip route`, `ping`, and `nslookup` to investigate network connectivity problems.

### 6. Cybersecurity Lab Preparation

Preparing an environment that can be expanded for authorized network scanning, vulnerability assessment, and security testing.

### 7. Technical Documentation

Learning the importance of documenting configurations, commands, screenshots, troubleshooting steps, and verification results.

---

## 🔐 Security and Ethical Use

This laboratory is intended for educational purposes and authorized security testing.

All scanning, testing, and exploitation activities must be restricted to systems you own or have explicit permission to assess.

Before conducting practical security exercises, verify that the target is part of the intended lab environment.

---

## 🔗 Tools and Resources

* [Oracle VirtualBox](https://www.virtualbox.org/wiki/Downloads)
* [Kali Linux](https://www.kali.org/get-kali/)
* [Nmap](https://nmap.org/)
* [GitHub](https://github.com/)

---

## 👤 Author

**Lucas Yona**

Cybersecurity Lab Setup Project

**Program:** Networkwalks Cybersecurity
**Week:** 01
**Project:** Cybersecurity Lab Environment Setup
**Repository:** GitHub

---

## 📌 Project Status

**Status:** In Progress — update after completing and verifying each configuration step.

### Completion Checklist

* [ ] VirtualBox installed and working.
* [ ] Kali Linux virtual machine starts successfully.
* [ ] NAT Network created with the required `10.0.0.0/24` subnet.
* [ ] Kali Linux connected to the correct NAT Network.
* [ ] Network interface configuration verified.
* [ ] Gateway connectivity tested.
* [ ] Internet connectivity tested.
* [ ] DNS resolution tested.
* [ ] Nmap installation verified.
* [ ] Required screenshots added.
* [ ] Troubleshooting notes completed.
* [ ] README updated to reflect the actual results.
* [ ] Clean virtual machine snapshot created, if required.

**Final Note:** This README should be updated as the project progresses so that it accurately reflects the configuration, tests, screenshots, and results of the actual laboratory.

