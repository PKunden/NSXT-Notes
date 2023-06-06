# NSX Edge and Cluster
This section is focused on NSX Edge and cluster. More on why we need Edge and how edge cluster adds value

## NSX Edge - Why do you need it ?
1. simple answer is - you need them to run SR.
2. N-S traffic i.e. traffic going outside SDDC
3. To run Dynamic routing protocols such BGP
4. Run a stateful services e.g. LB, FW and NAT
4. Enable service insertion with 3rd party vendors.

## Edge Cluster
Failure domains can be configured with NSX APIs and are used to automatically place the Tier-1 gateway active and standby instances. Failure domains guarantee service availability, for example, if a rack failure occurs. Active and standby Tier-1 gateway services always run in different failure domains.

## Networking

NSX Edge has minimum three networks configured and each need its own VLAN. In theory, you can place Edge on same management VLAN as ESXi.

1. Uplinks
2. TEP - overlay networks
3. Management

### Uplinks
You do not actually configure them directly when you deploy edge node. You just select the uplink profile. Inside the uplink profile you can define teaming policy and VLAN ID. These are the one which forms the Right and Left VLAN foundation. But then on Edge you create TEP as well. This TEP is the one required for routing traffic between Hypervisor and Edge node. You can use same VLAN but recommended is to use different VLAN. You need 2 VLANs for the uplink (Right VLAN and Left VLAN)

### IP
You need 5 Static IPs as mentioned below
1. Management (VLAN)
2. 2 x TEP (VLAN)
3. 1 X Right VLAN
4. 1 x Left VLAN
5. 1 x RTEP VLAN (NSX-T Federation)

TEP VLANs must be routable to Host TEP VLANs and must be separate VLAN than Host TEP VLANs
- Management is mapped to eth0
- TEP01 and Right VLAN is mapped to fp-eth0
- TEP02 and left VLAN is mapped to fp-eth1
- Then these are connected to Trunk Portgroups of vDS Switch. 
>In turn these are connected to trunk uplink portgroups on the VDS.

### Before you
Before you start deploying Edge, always remember that you need a Transport Zone based on VLAN. This transport zone must be VLAN based because on this transport zone you create Segments for the uplinks i.e.right and left VLAN.

### Transport Zone
An NSX Edge belongs to at least one VLAN transport zone to provide the uplink access. It can belong to multiple VLAN transport zone and but it can belong to only one Overlay transport zone.
When NSX Manager is deployed via VCF, it creates two transport zone
1. Overlay transport zone - all clusters in the domain are part of this transport zone
2. VLAN transport zone - but it is not used

when Edge is deployed, a dedicated VLAN transport zone is created.

>VCF bringup deploys an NSX-T Manager cluster and configures two new transport zones, which replace the built-in NSX-T default configuration. The first is an overlay transport zone which spans all clusters in the workload domain. The second is a VLAN transport zone that is not used by default. When an edge cluster is deployed, the NSX-T manager creates an additional transport zone which is dedicated to edge uplink connections, and an N-VDS which spans the cluster nodes and connects the edge nodes to both transport zones.

