<h1>Network Traffic Analysis</h1>

<h2>Description</h2>

The initial step involves connecting to a virtual private network (VPN) to begin network traffic analysis. This connection facilitates access to a live Virtual Machine (VM) host, enabling access to a Graphical User Interface (GUI). Through this setup, the goal is to use Wireshark, a deep and comprehensive analysis tool, within the environment to extract meaningful insights, actionable information, and suspicious traffic from the network traffic data.

https://github.com/angeloqmartin/Network-Traffic-Analysis/assets/37564935/15b94f60-eeb7-4fcf-bf2d-e7ecb33cf3ea

<h2>Analysis</h2>

The recent live traffic analysis revealed suspicious activity originating from within the network. Our immediate objective is to pinpoint the exact source of this questionable traffic.

1. Establishing Scope and Goal:
1.1. Objective: Identify the source of traffic originating from 10.129.43.4.
1.2 Timeframe: Analyzing traffic ongoing for the past 48 hours.
1.3 Supporting Information: Utilizing pcap file containing the exported results.


**Apply filter ip.host == 10.129.43.4
<img width="1440" alt="Screenshot 2023-12-08 at 12 12 23 PM" src="https://github.com/angeloqmartin/Network-Traffic-Analysis/assets/37564935/0c5c7cbb-d1d3-477c-b31f-e435f9f8966e">

<h2>Conversations</h2>

<img width="1185" alt="Screenshot 2023-12-08 at 1 19 07 PM" src="https://github.com/angeloqmartin/Network-Traffic-Analysis/assets/37564935/55d4e022-7f32-45cd-bce1-b5a50b5e95a6">

Following an examination of the conversations depicted above, it's noticeable that three conversations were captured, all directly associated with our suspicious host identified as 10.129.43.4. Our subsequent course of action involves inspecting the protocol hierarchy to gain insights into the nature and composition of this traffic.

<h2>Protocol Statistics</h2>

![Screenshot 2023-12-08 at 2 51 06 PM copy](https://github.com/angeloqmartin/Network-Traffic-Analysis/assets/37564935/962d214c-959f-4038-85c4-bd9b3fdba8bc)

The network traffic within this PCAP file primarily consists of TCP traffic, accompanied by a smaller portion of UDP traffic. Given the lesser prevalence of UDP compared to TCP, our initial focus will be on isolating and examining UDP traffic to uncover any anomalies. To streamline our analysis, we'll begin by filtering out all non-UDP traffic, aiming to identify and investigate any potentially unusual occurrences within this subset.

<h2>UDP</h2>

Apply filter !tcp
<img width="1376" alt="Screenshot 2023-12-08 at 3 46 00 PM" src="https://github.com/angeloqmartin/Network-Traffic-Analysis/assets/37564935/378bf087-5a51-41a2-92a2-cb108816e302">

The network traffic within this PCAP file primarily consists of TCP traffic, accompanied by a smaller portion of UDP traffic. Given the lesser prevalence of UDP compared to TCP, our initial focus will be on isolating and examining UDP traffic to uncover any anomalies. To streamline our analysis, we'll begin by filtering out all non-UDP traffic, aiming to identify and investigate any potentially unusual occurrences within this subset.

<h2>TCP</h2>

The following filter “!udp && !arp” will clear out anything we have already analyzed
<img width="1437" alt="Screenshot 2023-12-08 at 4 00 00 PM" src="https://github.com/angeloqmartin/Network-Traffic-Analysis/assets/37564935/2b20b9c8-ef9d-4b13-af55-4b415c94b233">

All the remaining packets within the dataset belong to the TCP protocol. Notably, these packets seem to constitute a single ongoing conversation between our specified target host, "10.129.43.4," and IP address 10.129.43.29. This determination is based on the observation of a session establishment through a three-way handshake, which occurs in packet 3. Additionally, the consistent usage of the same ports across the subsequent packets in the output further supports this ongoing communication between the specified hosts.

<h2>TCP Session Establishment</h2>

<img width="1376" alt="Screenshot 2023-12-08 at 4 19 05 PM" src="https://github.com/angeloqmartin/Network-Traffic-Analysis/assets/37564935/4203f868-ccb0-47e4-8a9f-ede6ee88d777">

A notable absence in this PCAP file is the lack of a TCP session "teardown." This absence suggests that the session might have remained active and not yet terminated, which is further supported by the absence of any Reset packets. To confirm and gain a deeper understanding, the next steps involve examining the conversation by tracing the TCP stream to comprehend the content and nature of this ongoing communication.

<h2>Follow TCP Stream</h2>

https://github.com/angeloqmartin/Network-Traffic-Analysis/assets/37564935/c0312edd-615e-47d1-9f09-90e3a0ed61d8

Upon inspecting the TCP stream, several concerning observations can be made. The entire conversation between the two hosts is in plain text, revealing that someone conducted various activities on the host. Upon reviewing the content further, it's evident that the actor was conducting basic reconnaissance of the host. They executed commands such as whoami, ipconfig, and dir. This indicates an attempt to survey and ascertain the user context they've landed in on the host as if trying to understand the environment and user privileges.

<img width="661" alt="Screenshot 2023-12-08 at 6 08 27 PM" src="https://github.com/angeloqmartin/Network-Traffic-Analysis/assets/37564935/74515698-459e-48c4-9c0c-450e3c22eb7d">

<h2>Summary and Remediation</h2>

<img width="711" alt="Screenshot 2023-12-09 at 12 32 23 AM" src="https://github.com/angeloqmartin/Network-Traffic-Analysis/assets/37564935/2a23ee68-d3eb-4ca6-ab51-5869c626db13">

The analysis reveals a troubling discovery: the creation of an account named "hacker" and its inclusion in the administrator's group on the host. This finding raises serious concerns as it could be an error by an inexperienced administrator or, more worryingly, a sign of unauthorized access and potential intrusion into the corporate infrastructure. Our analysis indicates the infiltration of at least one host on the network. Specifically, host 10.129.43.29 demonstrates evidence of command execution involving user creation and the assignment of local administrator permissions using "net" commands. This suggests that the actor might have been leveraging this host to perform these actions.

<h2>Remediation Action:</h2>

1. Isolate and Quarantine:
          * Immediately isolate the affected host 10.129.43.29 on the network to prevent further potential damage or unauthorized access.
3. Disable the Suspect Account:
          * Disable or remove the"hacker" account and any other suspicious accounts created on the compromised host.
4. Review User Permissions:
          * Conduct a thorough review of user accounts and permissions across the network, particularly within the administrator's group. Remove unauthorized access and limit privileges to necessary functionalities.
5. Forensic Analysis:
          * Perform in-depth forensic analysis on the compromised host and associated network logs to understand the extent of the intrusion and identify potential points of entry.
6. Patch and Update Systems:
          * Ensure that all systems, including software and applications, are up-to-date with the latest security patches and configurations to mitigate known vulnerabilities.
7. Implement Stronger Authentication Measures:
          * Enforce stronger password policies, multi-factor authentication, and access controls to enhance security and prevent unauthorized access.
8. Security Awareness Training:
          * Conduct security awareness training sessions for employees to educate them on identifying and reporting suspicious activities or security threats.
9. Incident Response Plan:
          * Review and update the incident response plan to include steps for handling similar security incidents promptly in the future.
10. Continuous Monitoring and Analysis:
          * Implement robust monitoring tools and practices to continuously analyze network traffic for any abnormal activities or potential threats.

These remediation actions should be carried out promptly and in coordination with the organization's IT security team to effectively mitigate the risks posed by the identified security breach.
