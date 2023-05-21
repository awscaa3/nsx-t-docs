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

When the connection between the Primary location and secondary location is down, then it is referred as split brain situation. In split brain situation, N-S traffic from Primary location is working but from the secondary location is not going to work. To fix this, manually change the primary location but in this case N-S traffic in primary location is impacted. So it is this or that but not both.
