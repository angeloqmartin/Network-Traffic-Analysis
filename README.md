<h1>Network Traffic Analysis</h1>

<h2>Description</h2>

The initial step involves connecting to a virtual private network (VPN) to begin network traffic analysis. This connection facilitates access to a live Virtual Machine (VM) host, enabling access to a Graphical User Interface (GUI). Through this setup, the goal is to use Wireshark, a deep and comprehensive analysis tool, within the environment to extract meaningful insights, actionable information, and suspicious traffic from the network traffic data.


https://github.com/angeloqmartin/Network-Traffic-Analysis/assets/37564935/15b94f60-eeb7-4fcf-bf2d-e7ecb33cf3ea


<h2>Analysis</h2>

The recent live traffic analysis revealed suspicious activity originating from within the network. Our immediate objective is to pinpoint the exact source of this questionable traffic.

1. Establishing Scope and Goal:
  - 1.1 Objective: Identify the source of traffic originating from 10.129.43.4.
  - 1.2 Timeframe: Analyzing traffic ongoing for the past 48 hours.
  - 1.3 Supporting Information: Utilizing pcap file containing the exported results.
2. Defining Targets:
  - 2.2 Focus: Investigating traffic associated with 10.129.43.4 and all connections to it, particularly unidentified protocol traffic using port 4444.
3. In-Depth Analysis of the PCAP File Capturing Network Traffic within the 10.129.43.0/24 network:
  - 3.1 Anticipate the presence of suspicious traffic within the captured data, specifically related to the suspected source.
4. Identifying Necessary Network Traffic Components (Filtering):
  - 4.1 Initial filtering will involve excluding any traffic not associated with connections to 10.129.43.4. This step prioritizes our investigation by concentrating on our primary suspicious target.

Apply filter ip.host == 10.129.43.4
<img width="1440" alt="Screenshot 2023-12-08 at 12 12 23 PM" src="https://github.com/angeloqmartin/Network-Traffic-Analysis/assets/37564935/0c5c7cbb-d1d3-477c-b31f-e435f9f8966e">


<h2>Conversations</h2>

<img width="1185" alt="Screenshot 2023-12-08 at 1 19 07 PM" src="https://github.com/angeloqmartin/Network-Traffic-Analysis/assets/37564935/55d4e022-7f32-45cd-bce1-b5a50b5e95a6">

Following an examination of the conversations depicted above, it's noticeable that three conversations were captured, all directly associated with our suspicious host identified as 10.129.43.4. Our subsequent course of action involves inspecting the protocol hierarchy to gain insights into the nature and composition of this traffic.

<h2>Protocol Statistics</h2>

![Screenshot 2023-12-08 at 2 51 06 PM copy](https://github.com/angeloqmartin/Network-Traffic-Analysis/assets/37564935/962d214c-959f-4038-85c4-bd9b3fdba8bc)

The network traffic within this PCAP file primarily consists of TCP traffic, accompanied by a smaller portion of UDP traffic. Given the lesser prevalence of UDP compared to TCP, our initial focus will be on isolating and examining UDP traffic to uncover any anomalies. To streamline our analysis, we'll begin by filtering out all non-UDP traffic, aiming to identify and investigate any potentially unusual occurrences within this subset.
