---
layout: page
title: Wireshark
description: Analyzing Network Traffic
img: assets/img/wiresharklogo.jpg
importance:
category: work
toc:
  sidebar: left
---

## Introduction

If you're entering the world of cybersecurity, network administration, or IT, Wireshark is an essential tool you'll come across. Known as one of the most powerful network protocol analyzers, Wireshark allows users to capture and inspect packets in real-time, providing insights into network traffic that can be invaluable for troubleshooting, performance monitoring, or investigating security incidents. This blog post will introduce you to Wireshark, its capabilities, and explain some real-world examples using screenshots from a packet capture (PCAP) file analysis.

## What is Wireshark?

Wireshark is an open-source network protocol analyzer that enables users to see what’s happening on their network at a microscopic level. It captures network packets and displays them in detail, allowing you to examine their contents and identify various protocols. Wireshark is widely used in industries such as cybersecurity, networking, and IT support due to its powerful features, including:

- **Packet Capture**: Captures live network traffic or analyzes previously saved captures.
- **Deep Packet Inspection**: Inspects protocols like TCP, UDP, HTTP, DNS, FTP, and more.
- **Filtering**: Applies display filters to focus on specific traffic patterns or types.
- **Statistics and Metrics**: Provides insights into protocol hierarchy, endpoints, and conversations.

Whether you're diagnosing network issues, inspecting suspicious traffic, or understanding protocol behavior, Wireshark is the tool of choice.

## Setting Up Wireshark

Before diving into analysis, let's briefly walk through setting up Wireshark:

1. **Download and Installation**: Wireshark can be downloaded for free from its [official site](https://www.wireshark.org/). It supports multiple platforms including Windows, macOS, and Linux.
2. **Starting a Capture**: Launch Wireshark, select the appropriate network interface (e.g., Wi-Fi, Ethernet), and click "Start Capture." Wireshark will begin capturing packets from the network.
3. **Applying Filters**: To narrow down the traffic and focus on specific types, use Wireshark's powerful display filters (e.g., `tcp`, `http`, or `ip.addr == 192.168.1.1`).

## Analyzing a PCAP File: A Walkthrough

To provide a hands-on example, we'll analyze a captured file named `web server.pcap`. This file captures network traffic related to a session between two hosts, revealing details about their interactions using protocols like TCP and SMB2. Let’s explore this step by step, referring to the screenshots below.

---

## Screenshot 1: Capture File Properties

![Wireshark Capture File Properties](wireshark1.jpeg)

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/wireshark1.jpeg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

In this screenshot, Wireshark provides an overview of the PCAP file properties:

- **File Information**: The file name is `web server.pcap`, with a size of 2283 KB and a snapshot length of 262,144 bytes, indicating the maximum size of captured packets.
- **Time Frame**: The capture started at `2023-09-10 11:13:06` and ended at `2023-09-10 11:27:37`, covering approximately 14 minutes of network activity.
- **Statistics**:
  - **Packets Captured**: 21,070 packets were captured in this timeframe.
  - **Average Packet Size**: The average packet size is 92 bytes, which is typical for SMB traffic where messages are often relatively small.
  - **Bytes per Second**: The capture shows an average throughput of 2,235 bytes per second.

This information provides context for the volume and nature of the traffic, helping an analyst estimate whether the amount of data exchanged aligns with expected behavior or indicates potential anomalies.

## Screenshot 2: Packet List View

![Wireshark Packet List View](wireshark2.png)

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/wireshark2.jpeg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

This screenshot shows the packet list for the `web server.pcap` file. The view highlights communication between two IP addresses: `10.0.0.115` (source) and `10.0.0.105` (destination). Key observations include:

- **TCP Handshake**: The initial packets represent a standard TCP three-way handshake, where the source IP initiates a connection to the destination on port 445 (commonly used for SMB/CIFS services).
- **SMB2 Protocol**: Following the TCP connection, the traffic shifts to the SMB2 protocol, which is used for file sharing and remote administration on Windows networks. The list shows session setup requests and tree connect requests—typical operations for accessing shared resources or IPC paths.
- **Error Messages**: Errors such as `STATUS_NOT_FOUND` indicate the client attempted to access a non-existent path, useful for troubleshooting file share or permissions issues.

## Screenshot 3: Protocol Hierarchy Statistics

![Wireshark Protocol Hierarchy Statistics](wireshark3.png)

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/wireshark3.jpeg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

This screenshot displays Wireshark's Protocol Hierarchy Statistics feature, providing a breakdown of the different protocols captured:

- **Ethernet and IPv4**: All captured packets are under Ethernet and IPv4 layers, confirming local IPv4 network traffic.
- **TCP (Transmission Control Protocol)**: TCP traffic constitutes the majority, which is expected as SMB2 operates over TCP.
- **SMB2 (Server Message Block version 2)**: SMB2 traffic is significant, highlighting that file-sharing operations dominate this session.
- **HTTP and SSH**: Minimal HTTP and SSH packets are also present, suggesting occasional web-based activities or secure remote access attempts.

The hierarchical view quickly reveals the protocol distribution, helping analysts focus on dominant or unexpected protocols.

## Screenshot 4: Conversations Overview

![Wireshark Conversations Overview](wireshark4.png)

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/wireshark4.jpeg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

In this screenshot, the Conversations view shows the communication between IP addresses, breaking down the volume of packets, bytes transferred, and conversation duration:

- **Top Conversations**: The main conversation is between `14.0.0.120` and `10.0.0.112`, with significant data exchange (2 MB).
- **Additional Details**: Smaller conversations are also visible, such as between `10.0.0.105` and `10.0.0.115`, which are relevant to understanding the file-sharing activities. The duration column provides insight into how long each conversation lasted, which can indicate the persistence or briefness of certain connections.

## Screenshot 5: Top IPs and Ports

![Wireshark Top IPs and Ports](wireshark5.png)

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/wireshark5.jpeg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

The final screenshot displays the top IPs and ports involved in the capture:

- **Top IP Addresses**: `14.0.0.120` and `10.0.0.115` are identified as the most active IPs in this capture, indicating they are key participants in the session.
- **Top Ports**: The ports `51985` and `6180` are highlighted, suggesting these were the primary ports used for communication. Understanding these details helps analysts determine which services or applications are involved and whether the traffic pattern is typical or suspicious.

## Why Use Wireshark?

Wireshark is invaluable in many professional settings. Whether you're monitoring a network for performance, identifying and mitigating potential attacks, or simply verifying network configuration, Wireshark provides the data needed to make informed decisions. Here are some use cases:

- **Troubleshooting Network Issues**: Analyze packet flows to identify latency issues, dropped connections, or misconfigured devices.
- **Security Analysis**: Detect suspicious activity like malware communication or unauthorized access attempts.
- **Protocol Analysis**: Understand how different protocols operate, making it easier to configure or debug network services.

## Conclusion

Wireshark is a must-have tool for anyone serious about network analysis, cybersecurity, or IT. Its ability to dissect traffic, provide detailed insights into protocols, and visualize network activity makes it essential for troubleshooting, forensics, and performance monitoring.

This post aimed to introduce Wireshark through the analysis of a sample PCAP file. By exploring the details of this capture, we learned about TCP handshakes, SMB2 protocol interactions, and common errors that can be detected through packet inspection. I encourage you to download Wireshark and try capturing your own network traffic to gain hands-on experience!

If you're looking to add network analysis skills to your toolkit or further your career in IT or cybersecurity, mastering Wireshark is a great step forward.
