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

### Uplinks
You do not actually configure them directly when you deploy edge node. You just select the uplink profile. Inside the uplink profile you can define teaming policy and VLAN ID. These are the one which forms the Right and Left VLAN foundation. But then on Edge you create TEP as well. This TEP is the one required for routing traffic between Hypervisor and Edge node. You can use same VLAN but recommended is to use different VLAN.

### Before you
before you start deploying Edge, always remember that you need a Transport Zone based on VLAN. This transport zone must be VLAN based because on this transport zone you create Segments which again have right and left VLAN concept.
