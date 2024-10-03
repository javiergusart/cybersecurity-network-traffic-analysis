# Analyzing Network Layer Communication: DNS and ICMP Traffic Issues

## Table of Contents
- [Introduction](#introduction)
- [The Investigation](#the-investigation)
- [Network Analysis](#network-analysis)
- [Analysis of the Logs](#analysis-of-the-logs)
- [Key Findings from the Analysis](#key-findings-from-the-analysis)
- [Conclusion](#conclusion)

## Introduction

In this activity, I analyzed DNS (Domain Name System) and ICMP (Internet Control Message Protocol) traffic related to the website **www.yummyrecipesforme.com**, a fictional example used for educational purposes. The website faced accessibility issues that resulted in a "destination port unreachable" error for several users. The goal was to identify potential causes of this error and assess the affected network protocols. This analysis was part of the Google Cybersecurity Professional Certificate program's Connect and Protect: Networks and Network Security course.

After multiple clients reported being unable to access the website, I encountered the same "destination port unreachable" error during the investigation. This led to a deeper analysis of the DNS and ICMP traffic. DNS is responsible for translating human-readable domain names into IP addresses, while ICMP is used to send error messages and operational information about network communications. By utilizing the **tcpdump** network protocol analyzer, I gained insights into the potential issues affecting these protocols.

## The Investigation

My goal was to determine why the website was inaccessible. To begin, I used the network protocol analyzer **tcpdump** to capture network traffic. **tcpdump** is a command-line packet analyzer used to capture and display network packets, providing insights into the behavior of network protocols. When my browser sent a DNS request to resolve the domain name of the website, it used the **UDP (User Datagram Protocol)**, a communication protocol used for sending short messages called datagrams. However, the response indicated that the request was unsuccessful.

## Network Analysis

![LKXsnNIhT0e1mAz5AEvxog_d363c94e0a4f4a8b90b0be403f6ee1f1_mMBaLWLyXG2omYBcSdjuR8y5_S59zow1ZEPYdjNyJzA1B0r55nI9KmDosI8QHXcEwE51NxM3N5gNtMgSOyVDHyJVLZvZA7_jJtkzUKfxuqFUJPHs57vVVES-LbG5teR8eir4idaqsxFaYJhhVJZn-a_S-txb7zQNIZq07XESgSkqDHuzfvALfYk3lipGVBY](https://github.com/user-attachments/assets/fdcdc841-bc31-4d9b-805e-2e3c04e1514b)

Upon analyzing the tcpdump logs, I found that the requests sent to the DNS server were met with **ICMP error messages** stating **"udp port 53 unreachable."** This indicates that the DNS server was either down or blocking requests on **port 53**, which is the default port used by DNS to listen for incoming queries and respond to them. If a server is unreachable on port 53, DNS queries cannot be resolved, making websites inaccessible.

## Analysis of the Logs

| **Summary**                             | **Details**                                                                 |
|-----------------------------------------|-----------------------------------------------------------------------------|
| **UDP protocol activity**               | Multiple DNS queries were sent to the DNS server (IP: 203.0.113.2) via UDP port 53. |
| **ICMP error messages**                 | The logs contained ICMP messages indicating that the UDP packets couldn’t reach port 53 of the DNS server. |
| **Port 53 purpose**                     | Port 53 is used for DNS queries, allowing DNS servers to receive and respond to requests.                                             |
| **Possible issues**                     | A DNS server failure, firewall misconfiguration, or a Denial-of-Service (DoS) attack may be preventing the server from processing requests. |

The analysis revealed that DNS queries were consistently sent to the DNS server, but the server did not respond. The presence of ICMP error messages indicates that the communication channel between the client and the DNS server was disrupted. This could be due to the server being offline, a firewall blocking traffic on port 53, or a more serious issue like a DoS attack, which overwhelms the server with requests, making it unable to respond to legitimate traffic.

## Key Findings from the Analysis

| **Finding**                              | **Details**                                                                 |
|------------------------------------------|-----------------------------------------------------------------------------|
| **Time of Incident**                     | The issue occurred on October 2, 2024, at 13:24:32.                         |
| **How the Issue Was Detected**           | Users reported not being able to access the website.                        |
| **Steps Taken by the IT Department**     | The IT team used tcpdump to capture and analyze the network traffic.        |
| **Findings from the Investigation**      | The DNS server was unreachable on port 53, which blocked DNS resolution.    |
| **Likely Causes**                        | The DNS server was likely down due to failure, misconfigured firewalls, or a DoS attack. |

The investigation confirmed that the DNS server was unreachable, preventing users from accessing the website. The analysis highlighted that various factors could have led to this situation, including the possibility of server downtime, misconfigurations in the firewall settings, or a potential Denial-of-Service (DoS) attack targeting the DNS server. Understanding these findings is crucial for developing effective remediation strategies.

## Conclusion

This analysis provided valuable hands-on experience with diagnosing DNS and ICMP traffic issues. It highlighted vulnerabilities within the DNS infrastructure that need attention to avoid further accessibility issues. Throughout the process, I identified critical areas where improvements should be made, especially in how DNS requests are handled.

Reflecting on this experience, I gained insights into the importance of carefully analyzing network traffic logs. It also deepened my understanding of how seemingly small misconfigurations or outages can cause widespread accessibility problems.

Furthermore, this investigation reinforced the need for continuous monitoring and incident response. The lessons learned will be essential as I continue to develop my skills in cybersecurity.
