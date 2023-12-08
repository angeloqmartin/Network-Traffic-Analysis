<h1>Network Traffic Analysis</h1>

<h2>Description</h2>

The initial step involves connecting to a virtual private network (VPN) to begin network traffic analysis. This connection facilitates access to a live Virtual Machine (VM) host, enabling access to a Graphical User Interface (GUI). Through this setup, the goal is to use Wireshark, a deep and comprehensive analysis tool, within the environment to extract meaningful insights, actionable information, and suspicious traffic from the network traffic data.


https://github.com/angeloqmartin/Network-Traffic-Analysis/assets/37564935/15b94f60-eeb7-4fcf-bf2d-e7ecb33cf3ea


<h2>Analysis</h2>

The recent live traffic analysis revealed suspicious activity originating from within the network. Our immediate objective is to pinpoint the exact source of this questionable traffic.

1. Establishing Scope and Goal:
  - 1.1 Objective: Identify the source of traffic originating from 10.129.43.4.
  - 1.2 Timeframe: Analyzing traffic ongoing for the past 48 hours.
  - 1.3 Supporting Information: Utilizing the NTA.pcap file containing the exported results.
2. Defining Targets:
  - 2.2 Focus: Investigating traffic associated with 10.129.43.4 and all connections to it, particularly unidentified protocol traffic using port 4444.
3. In-Depth Analysis of the PCAP File Capturing Network Traffic within the 10.129.43.0/24 network:
  - 3.1 Anticipate the presence of suspicious traffic within the captured data, specifically related to the suspected source.
4. Identifying Necessary Network Traffic Components (Filtering):
  - 4.1 Initial filtering will involve excluding any traffic not associated with connections to 10.129.43.4. This step prioritizes our investigation by concentrating on our primary suspicious target.
