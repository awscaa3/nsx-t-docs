## Network Data Plane Recovery

The loss of one location does not inevitably generates a data plane failure.

**Without Services**

If the Tier-0 is stretched without stateful services (no NAT and no GW-FW) and Tier-1 is configured without Edge Clusters for services, then the data plane automatically recovers.

**With Services**

If the Tier-0 or Tier-1 are stretched with services (NAT and/or GW-FW), then **only** the loss of the Tier-0 or Tier-1 primary location will generate a data plane failure. To recover the data plane, a manually action/move is required to move the Tier-0 or Tier-1 primary location to another location.

### Automatic Network Data Plane Recovery – Tier-0 without services (No NAT / No GW-FW) and Tier-1 stretched without Edge Clusters

There are two Tier-0 / Tier-1 stretched network topologies without services (no NAT / No GW-FW) which offer automatic data plane recovery in case of any location loss.

#### T0 A/A Loc P/S + T1-Streched DR_Only

In this topology Tier-0 is Active/Active with Location Primary/Secondary connected to a Tier-1 DR_Only.

#### T0 A/A Loc All_P + T1-Streched DR_Only

In this topology, Tier-0 is active-active in all location and as well primary in all location.

---

### Manual Network Data Plane Recovery – Tier-0 or Tier-1 stretched with services (NAT / GW-FW)

In this scenario, only manual recovery is possible as either T1 or T0 is running stateful services. There are four Tier-0 / Tier-1 stretched network topologies with services (NAT / GW-FW). Those which offer automatic data plane recovery in case of any location loss.

#### T0 A/S Loc P/S + T1-Streched DR_Only

In this topology T0 is active-standby and T1 is only running only DR services. It means there are not services running on it. When the Primary location is down, it means Tier-0 is lost, therefore in this scenario the data plane requires manually recovery because N-S traffic is impacted. 

**To recover North/South traffic, the Tier-0 Primary location configuration must be changed from Location-A to Location-B**

When the connection **between** the Primary location and secondary location is down, then it is referred as split brain situation. In split brain situation, N-S traffic from Primary location is working but from the secondary location is not going to work. To fix this, manually change the primary location but in this case N-S traffic in primary location is impacted. So it is this or that but not both.

#### T0 A/S Loc P/S + T1 A/S Loc P/S

In this scenario, services are configured on T1 and possible as well on T0. This topology is with stretched Tier-0 Active/Standby Location Primary/Secondary connected to a Tier-1 Active/Standby Location Primary/Secondary.

When the primary location is down, T0 and T1 are not reachable. In this case, manual recovery is must. As there is no more advertisement of the internal subnet to the physical fabricBecause the North South traffic is broken. To restore North/South traffic, the Tier-0 and Tier-1 Primary location configuration must be changed from Location-A to Location-B

#### T0 A/A Loc P/S + T1 A/S Loc P/S

Here there are no services configured on T0 but services are configured on T1. This topology is with stretched Tier-0 Active/Active Location Primary/Secondary connected to a Tier-1 Active/Standby Location Primary/Secondary.

The loss of Location-A (Tier-0 and Tier-1 Primary location) brings the entire Location-A down: its Compute, its Network and Security, and its LM. The best advertisement of the internal subnet is now via Location-B. The Tier-0 (unsure if it is T1 or T0, in my opinion it should be T1) in Location-B will receive it but then it will forward it to the Tier-1 Primary location (Location-A) breaking North/South traffic.

As in the above case, T0 and T1 primary location must be changed from Location-A to Location-B

#### T0 A/A Loc All_P + T1 A/S Loc P/S

In this scenario all T0 are active plus there are primary in all locations and T1 as describe above. Since the primary T1 are located in the Location-A, N-S traffic will exit out and enter in via Location-A. In case when location A is down, N-S traffic is impacted because T1 secondary always sends traffic to T1 primary. If T1 Primary is down, N-S is impacted.

The recovery procedure is same as discussed above.
