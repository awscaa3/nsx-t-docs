# Requirements and Limitations

Here the requirements and limitations of NSX-T are discussed.

### Licensing and Version requirement

- NSX-T Enterprise plus on LM
- NSX-T 3.2 and above

### Infrastructure Requirements

* VIP for LM. Currently the LM Cluster VIP (or FQDN LM Cluster VIP) must be provided to allow the GM to LM communication to keep on even after one LM Management VM failure. LM should be registered using VIP
* 150 millisecond latency between sites
* MTU 9000
* Management Plane traffic should be prioritize using QoS
* Not NAT for the management traffic
  * LM to GM
  * LM to LM
  * RTEP to RTEP
* 

## Limitations

* GM-Active does not sync vIDM configuration with GM-Standby
* Containers (Containers have no concept of Locations. Network and Security services for Containers can be offered directly by LM; even with LM registered to GM)

### Features not supported

* Port Mirroring
* IPFIX
* Live Traffic Analysis
* Consolidated Capacity
* EVPN + Routing VRF
* Multicast
* OSPF
* DHCP Dynamic Binding

### Security Features

StretchedGroups based on SegmentPorts or Segment Ports Tag do not support VM cold vMotion / SRM across locations

The following security features are not supported

* URL Filtering
* Time-Based Firewall
* Identity Firewall
* Distributed IDS
* Gateway IDS/IPS
* Malware Prevention
* Network Detection and Response
* Network Introspection
* Endpoint Protection
* Distributed Security for vCenter VDS Port Group (using GM dynamic group membership based on LM VDS Port Group Tags)
* TLS inspection
