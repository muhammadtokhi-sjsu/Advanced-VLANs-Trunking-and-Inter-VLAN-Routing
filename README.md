# Lab 2: Advanced VLANs, Trunking, and Inter-VLAN Routing

This lab demonstrates configuration and verification of **VLANs**, **802.1Q trunking**, and **inter-VLAN routing** using Cisco switches and routed interfaces / SVIs in Cisco Packet Tracer.

---

## Task 1: VLAN Verification

### S1: `show vlan brief`

![VLAN Brief Output](lab2-vlan-brief.png)

### S2: `show vlan brief`

![VLAN Brief Output](lab2-vlan-brief-s2.png)

The `show vlan brief` command confirms that:
- All required VLANs (e.g., VLAN 10, VLAN 20, VLAN 30) are created.  
- Access ports are correctly assigned to the appropriate VLANs.  

Key checkpoints:
- Each PC-facing switchport is in the correct VLAN.  
- No user ports remain in the default VLAN unless intentionally configured.

---

## Task 2: Trunk Status (`show interfaces trunk` on S1 & S2)

### Switch S1 Trunks

![S1 Show Interfaces Trunk](lab2-s1-show-interfaces-trunk.png)

The `show interfaces trunk` output on S1 should verify:
- Trunk ports (e.g., `Fa0/1`, `Fa0/2`) are in **trunk** mode.  
- Encapsulation is **802.1Q** (dot1q), if manually configurable on the platform.  
- The **allowed VLAN list** includes all VLANs that must span between S1 and S2.

### Switch S2 Trunks

![S2 Show Interfaces Trunk](lab2-s2-show-interfaces-trunk.png)

On S2, `show interfaces trunk` confirms:
- Matching trunk configuration toward S1 and the inter-VLAN router / L3 switch.  
- The same VLANs are allowed and active on the trunk.  
- There are no unexpected pruning or VLAN mismatches on the link.

---

## Task 3: Inter-VLAN Connectivity (PC1 ↔ PC2 ↔ PC3)

### Ping Tests Between VLANs

![Ping PC1 to PC2](lab2-ping-pc1-to-pc2.png)

![Ping PC1 to PC3](lab2-ping-pc1-to-pc3.png)

Successful pings from **PC1** (in one VLAN) to **PC2** and **PC3** (in other VLANs) confirm:
- Inter-VLAN routing is configured correctly (via **router-on-a-stick** or **SVIs**).  
- Default gateways on each PC point to the correct VLAN interface IP.  
- VLAN tagging on trunks is working end-to-end.

### Full Mesh Ping Tests

- PC1 pinging all other PCs.  

![Ping Matrix PC1 and PC2](lab2-ping-matrix-pc1.png)

- PC2 pinging all other PCs.  

![Ping Matrix PC1 and PC2](lab2-ping-matrix-pc2.png)

These tests show:
- All PCs in different VLANs can reach each other through the L3 device.  
- There are no misconfigured access ports or missing VLANs on trunks.  
- The inter-VLAN routing path is symmetric and stable for all hosts.

---

## Commands Used (Reference)

Some commonly used verification commands in this lab:

