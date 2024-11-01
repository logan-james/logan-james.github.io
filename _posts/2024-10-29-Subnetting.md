---
layout: post
title: Understanding Subnetting
description: Sharing wonderful resources to understand subnetting.
tags: Networking
thumbnail: assets/img/sn1.png
importance:
category: CCNA
#related_publications: true
toc:
  sidebar: left
---

---

<p style="font-size: 0.7em;">
<strong>Note</strong>: This blog post compiles everything I've been learning about subnetting with the invaluable help of two fantastic resources: <em>Practical Networking</em> and <em>Jeremy's IT Lab</em>. Their clear explanations and hands-on examples have been essential in building my understanding. If you're diving into networking and subnetting, I highly recommend checking them out:
</p>

<ul style="font-size: 0.7em;">
    <li><a href="https://www.practicalnetworking.net/">Practical Networking</a>: Visit their website or explore their <a href="https://www.youtube.com/playlist?list=PLIFyRwBY_4bQUE4IB5c4VPRyDoLgOdExE">YouTube Subnetting Playlist</a> for detailed breakdowns of subnetting concepts.</li>
    <li><a href="https://www.jeremysitlab.com/">Jeremy's IT Lab</a>: Their site has plenty of resources, and their <a href="https://www.youtube.com/watch?v=H8W9oMNSuwo&list=PLxbwE86jKRgMpuZuLBivzlM8s2Dk5lXBQ">YouTube CCNA Playlist</a> is a must-watch for anyone pursuing CCNA certification.</li>
</ul>

<p style="font-size: 0.7em;">
Thanks to these resources, I've been able to build a strong foundation in subnetting, and I hope this post helps to share what I’ve learned!
</p>

---

## What is Subnetting?

Subnetting is a method used to divide a large network into smaller, more manageable subnetworks or "subnets." Each device in an IP network requires a unique IP address to communicate. Instead of assigning all devices in a large organization a single, massive network range, subnetting allows network administrators to create smaller, organized network segments.

These smaller networks help improve network efficiency, enhance security, and optimize IP address usage. By segmenting a network, administrators can control traffic flow and isolate different departments, locations, or functional areas. Subnetting is particularly essential with IPv4 addresses, where address space is limited.

In subnetting, each subnet is identified by a unique subnet mask, which defines how many addresses are available within that subnet. For example:

- A `/24` subnet mask provides 256 IP addresses.
- A `/27` subnet mask provides 32 IP addresses.

The subnet size is determined by the number of devices that need IP addresses in each segment. In the sections below, we'll visually break down how subnetting works and explore different subnet sizes.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/sn1.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/sn2.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/sn3.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
  <div class="caption">
     Visualizing Subnetting with the 10.0.0.x Range.
     To better understand how subnetting works, let’s look at the `10.0.0.x` IP address range. The images above illustrate different ways this range can be divided, showing the impact of using various subnet sizes. 
  </div>
</div>

#### Full IP Range: 10.0.0.0 to 10.0.0.255

The **first image** shows the entire `10.0.0.x` range, from `10.0.0.0` to `10.0.0.255`, covering 256 IP addresses. This setup is often referred to as a **/24 subnet** (255.255.255.0), allocating 8 bits for host addresses. Here’s what each part represents:

- `10.0.0.0` is the **Network ID**.
- `10.0.0.255` is the **Broadcast Address**.
- IP addresses from `10.0.0.1` to `10.0.0.254` are assignable to individual devices.

A `/24` subnet is ideal for medium-sized networks, allowing up to 254 devices in one segment.

#### Highlighting the /24 Subnet

The **second image** explicitly marks this `10.0.0.x` range as a `/24` subnet, reinforcing the concept of a `/24` network where the first three octets (`10.0.0`) represent the network portion, and the last octet is assigned to individual hosts.

Using a `/24` subnet mask ensures all addresses from `10.0.0.0` to `10.0.0.255` remain in one network segment. This is useful when you want devices to communicate within the same network. However, if fewer devices are needed, dividing the network further can be more efficient.

#### Splitting into /25 Subnets

The **third image** splits the `10.0.0.x` range into two **/25 subnets**, each with 128 addresses:

- The **first /25 subnet**: `10.0.0.0` to `10.0.0.127`
  - Network ID: `10.0.0.0`
  - Broadcast Address: `10.0.0.127`
  - Usable IP range: `10.0.0.1` to `10.0.0.126`
- The **second /25 subnet**: `10.0.0.128` to `10.0.0.255`
  - Network ID: `10.0.0.128`
  - Broadcast Address: `10.0.0.255`
  - Usable IP range: `10.0.0.129` to `10.0.0.254`

Each `/25` subnet has 126 usable IP addresses. This division is useful for smaller segments, allowing for better IP address management within the same `10.0.0.x` range.

---

### Seven Attributes of Subnetting

Understanding subnetting involves knowing the key attributes that define each subnet. These attributes help network administrators organize and manage IP address spaces efficiently. Let's go through each attribute:

<table style="width: 100%; border-collapse: collapse; text-align: left;">
    <thead>
        <tr>
            <th style="padding: 8px; border-bottom: 2px solid #ddd;">Attribute</th>
            <th style="padding: 8px; border-bottom: 2px solid #ddd;">Description</th>
            <th style="padding: 8px; border-bottom: 2px solid #ddd;">Example</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td style="padding: 8px; border-bottom: 1px solid #ddd;">Network ID</td>
            <td style="padding: 8px; border-bottom: 1px solid #ddd;">Starting IP address of the subnet. Represents the entire subnet.</td>
            <td style="padding: 8px; border-bottom: 1px solid #ddd;">10.0.0.0 (for 10.0.0.0/24)</td>
        </tr>
        <tr>
            <td style="padding: 8px; border-bottom: 1px solid #ddd;">Broadcast IP</td>
            <td style="padding: 8px; border-bottom: 1px solid #ddd;">Last IP address in the subnet. Used to send data to all devices within the subnet.</td>
            <td style="padding: 8px; border-bottom: 1px solid #ddd;">10.0.0.255 (for 10.0.0.0/24)</td>
        </tr>
        <tr>
            <td style="padding: 8px; border-bottom: 1px solid #ddd;">First Host IP</td>
            <td style="padding: 8px; border-bottom: 1px solid #ddd;">First usable IP address within the subnet, just above the Network ID.</td>
            <td style="padding: 8px; border-bottom: 1px solid #ddd;">10.0.0.1 (for 10.0.0.0/24)</td>
        </tr>
        <tr>
            <td style="padding: 8px; border-bottom: 1px solid #ddd;">Last Host IP</td>
            <td style="padding: 8px; border-bottom: 1px solid #ddd;">Last usable IP address in the subnet, just before the Broadcast IP.</td>
            <td style="padding: 8px; border-bottom: 1px solid #ddd;">10.0.0.254 (for 10.0.0.0/24)</td>
        </tr>
        <tr>
            <td style="padding: 8px; border-bottom: 1px solid #ddd;">Next Network</td>
            <td style="padding: 8px; border-bottom: 1px solid #ddd;">Starting IP address of the subsequent subnet, based on the current range.</td>
            <td style="padding: 8px; border-bottom: 1px solid #ddd;">10.0.1.0 (next after 10.0.0.0/24)</td>
        </tr>
        <tr>
            <td style="padding: 8px; border-bottom: 1px solid #ddd;"># IP Addresses</td>
            <td style="padding: 8px; border-bottom: 1px solid #ddd;">Total IP addresses in the subnet, including Network ID and Broadcast IP.</td>
            <td style="padding: 8px; border-bottom: 1px solid #ddd;">256 (for /24 subnet, with 254 usable)</td>
        </tr>
        <tr>
            <td style="padding: 8px; border-bottom: 1px solid #ddd;">CIDR/Subnet</td>
            <td style="padding: 8px; border-bottom: 1px solid #ddd;">CIDR notation specifies the subnet mask, defining the network and host bits.</td>
            <td style="padding: 8px; border-bottom: 1px solid #ddd;">/24 (for subnet mask 255.255.255.0)</td>
        </tr>
    </tbody>
</table>

1. **Network ID**

   - The Network ID (or Network Address) is the starting IP address of a subnet. It uniquely identifies the subnet within a larger network. This address cannot be assigned to a device, as it represents the entire subnet rather than an individual host.
   - For example, in a `10.0.0.0/24` subnet, `10.0.0.0` is the Network ID.

2. **Broadcast IP**

   - The Broadcast IP is the last address in the subnet and is used to send data to all devices within that subnet. When a device sends data to the Broadcast IP, all devices in the subnet receive the data.
   - In a `10.0.0.0/24` subnet, the Broadcast IP is `10.0.0.255`.

3. **First Host IP**

   - The First Host IP is the first usable IP address within a subnet, which can be assigned to a device. It’s one IP address above the Network ID.
   - In a `10.0.0.0/24` subnet, the First Host IP is `10.0.0.1`.

4. **Last Host IP**

   - The Last Host IP is the last usable IP address in the subnet, just before the Broadcast IP. This address can also be assigned to a device.
   - In a `10.0.0.0/24` subnet, the Last Host IP is `10.0.0.254`.

5. **Next Network**

   - The Next Network address is the starting IP of the subsequent subnet, based on the current subnet’s range. Knowing this helps prevent overlapping subnets and enables smooth address allocation when designing networks.
   - For a `10.0.0.0/24` subnet, the Next Network could start at `10.0.1.0` if we are allocating another `/24` block right after.

6. **# IP Addresses**

   - This attribute represents the total number of IP addresses within the subnet, including the Network ID and Broadcast IP. The number of usable IPs for hosts is the total number of IP addresses minus two (for the Network ID and Broadcast IP).
   - For a `/24` subnet, there are 256 IP addresses in total, with 254 usable IPs.

7. **CIDR/Subnet**
   - CIDR (Classless Inter-Domain Routing) notation specifies the subnet mask, which determines the size of the subnet. The subnet mask tells us how many bits are allocated to the network portion and how many bits are for hosts.
   - For example, `/24` indicates that 24 bits are used for the network, leaving 8 bits for hosts.

These seven attributes form the foundation of subnetting, helping network administrators allocate IP addresses effectively, maintain organized networks, and avoid conflicts. By understanding each attribute, you can better design and manage networks tailored to specific needs.

---

### Subnetting Cheat Sheet: Quick Reference Guide

This cheat sheet is a helpful tool for determining subnet sizes, subnet masks, and CIDR notations. By following a few simple steps, you can quickly identify the information needed for subnetting without complex calculations. Let's break down the steps and what each row represents.

#### Steps to Use the Cheat Sheet

1. **Start with 1 and Double**:

   - Begin with the number 1 and double it repeatedly, moving from right to left, until you reach 128. This forms the **Group Size** row at the top, indicating how many IP addresses each subnet size can provide.

2. **Subtract from 256**:

   - Take each number in the **Group Size** row and subtract it from 256 to get the values in the **Subnet Mask** row. This gives the subnet mask in the fourth octet for each subnet size, which is essential for IP addressing.

3. **List CIDR Notation**:
   - Start with `/32` on the right and move left, decreasing the CIDR notation by 1 for each column. The **CIDR** row specifies how many bits are used for the network portion of the address.

#### Cheat Sheet Breakdown

<table style="width: 100%; text-align: center; border-collapse: collapse;">
    <thead>
        <tr>
            <th style="padding: 8px; border-bottom: 1px solid #ddd;">Group Size</th>
            <th style="padding: 8px; border-bottom: 1px solid #ddd;">Subnet Mask</th>
            <th style="padding: 8px; border-bottom: 1px solid #ddd;">CIDR</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td style="padding: 8px;">128</td>
            <td style="padding: 8px;">128</td>
            <td style="padding: 8px;">/25</td>
        </tr>
        <tr>
            <td style="padding: 8px;">64</td>
            <td style="padding: 8px;">192</td>
            <td style="padding: 8px;">/26</td>
        </tr>
        <tr>
            <td style="padding: 8px;">32</td>
            <td style="padding: 8px;">224</td>
            <td style="padding: 8px;">/27</td>
        </tr>
        <tr>
            <td style="padding: 8px;">16</td>
            <td style="padding: 8px;">240</td>
            <td style="padding: 8px;">/28</td>
        </tr>
        <tr>
            <td style="padding: 8px;">8</td>
            <td style="padding: 8px;">248</td>
            <td style="padding: 8px;">/29</td>
        </tr>
        <tr>
            <td style="padding: 8px;">4</td>
            <td style="padding: 8px;">252</td>
            <td style="padding: 8px;">/30</td>
        </tr>
        <tr>
            <td style="padding: 8px;">2</td>
            <td style="padding: 8px;">254</td>
            <td style="padding: 8px;">/31</td>
        </tr>
        <tr>
            <td style="padding: 8px;">1</td>
            <td style="padding: 8px;">255</td>
            <td style="padding: 8px;">/32</td>
        </tr>
    </tbody>
</table>

#### Understanding Each Row

- **Group Size**: This row shows the number of IP addresses each subnet size offers. For example, a `/25` subnet provides 128 IP addresses, while a `/30` subnet offers only 4.
- **Subnet Mask**: The subnet mask row lists the decimal values of the subnet mask for each subnet size in the last octet. For instance, a `/27` subnet has a subnet mask of `255.255.255.224`.
- **CIDR**: The CIDR notation indicates the number of bits used for the network portion. As the CIDR number increases (moving from `/25` to `/32`), the number of usable IP addresses decreases, making the subnet smaller.

#### Using the Cheat Sheet for Quick Calculations

This cheat sheet is designed to make subnetting quicker and easier:

- If you need a subnet that supports up to 32 IP addresses, you can look at the `Group Size` row and see that a `/27` subnet is appropriate.
- For a subnet mask, if you know you need `/28`, you can see from the **Subnet Mask** row that it corresponds to `255.255.255.240`.

By following this cheat sheet, you can efficiently choose the correct subnet size, subnet mask, and CIDR notation based on your IP address requirements without needing complex calculations. It’s a great tool for both beginners and experienced network professionals!

---

### Another Way to Think About Subnetting: Binary Representation

To deepen our understanding of subnetting, it’s helpful to think of IP addresses in both their decimal and binary forms. By converting IP addresses from decimal to binary, we can clearly visualize which bits represent the **network** and which represent the **hosts**. In this example, we use the `203.0.113.0/27` subnet to illustrate this approach.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/sn6.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

In the binary representation:

- **Blue bits** represent the **network portion** of the IP address.
- **Red bits** represent the **host portion** of the IP address.
- **Purple bits** represent the **borrowed bits** that extend the network portion, allowing us to create additional subnets.

#### Breaking Down the Example: 203.0.113.0/27

In this example, the subnet `203.0.113.0/27` is represented in binary to show how the address is divided:

1. **Network Portion**: The first 27 bits (in blue and purple) represent the network portion of the IP address. This means that 27 bits are fixed and used to identify the network.
2. **Borrowed Bits**: To create a `/27` subnet, 3 bits (highlighted in purple) are borrowed from the host portion of the address. Borrowing these bits allows us to create smaller subnets within the larger network, providing more control over IP allocation.
3. **Host Portion**: The remaining 5 bits (in red) are left for host addresses within this subnet. With 5 bits for hosts, we can calculate the number of usable IP addresses as follows:

   \[
   2^5 - 2 = 30 \text{ usable addresses}
   \]

   Here, we subtract 2 to account for the **Network ID** and **Broadcast Address**, which cannot be assigned to individual devices.

#### Subnet Mask in Decimal

The subnet mask for a `/27` subnet is `255.255.255.224`, as shown in the binary representation:

- The first three octets are fully occupied by network bits (`255` in decimal).
- The fourth octet has the first 3 bits set to `1` (network) and the remaining 5 bits set to `0` (host), resulting in `224` in decimal.

---

## Summary of Subnetting Concepts

Subnetting is a fundamental networking skill that allows us to divide larger networks into smaller, efficient segments. By understanding how network and host bits are assigned, subnet masks, CIDR notation, and the various attributes of a subnet, we can effectively manage IP addresses, enhance network security, and control data flow within an organization. Through visual aids and binary representations, we’ve explored how subnetting transforms an IP address range to meet specific network requirements, from `/24` to `/27` subnets and beyond.

### Additional Resources for Practice

To further solidify your subnetting skills, here are some excellent resources where you can practice and test your knowledge:

- [Subnet IPv4 Practice](https://subnetipv4.com/)
- [Subnetting Practice](https://subnettingpractice.com/)

These sites offer exercises and quizzes to help you master subnetting concepts, making them a valuable addition to your study routine.
