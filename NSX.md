### Something about T1 and T0
- T1 requires an edge cluster if centralized services are configured. Otherwise there is no need of having Edge nodes
- T0 required edge nodes.
- An NSX Edge node is not a router.  It is a pool of services that is consumable by stateful services.
- Tier0 can be configured as Active/Active, up to 8 nodes in a cluster are allowed. Up to 8 of these can have uplink interfaces.
- Tier0 configured as Active/Standby, up to 2 nodes in a cluster are allowed. Total Edge Nodes cannot exceed 10. Up to 2 of these Total Edge Nodes can have uplink interfaces.

### Edge Clusters
1. Edge cluster is collection of edge nodes.
2. Edge cluster provides redundancy and scalability
3. Edge nodes provides compute for T0 and T1
4. Edge node can host only one T0 Gateway
5. An Edge cluster can have 10 nodes

### T0 Gateway uplink connection
1. you can have one or multiple Uplinks per NSX Edge
2. with multiple uplinks, you can have right and left VLAN

### Gateway components

Gateway has Service and router component and referred as
1. Service Router (SR)
2. Distributed Router (DR)

#### Distributed Router
- It is on all transport nodes i.e. on ESXi hosts and Edge nodes. But when services are enabled on T1, then T0 DR component is not distributed on ESXi hosts.
- It act as packet forwarder
- It runs as kernel module in the Hypervisor
- The moment you create gateway, DR is by default created.

#### Service Router
- Provides N-S Routing
- It is by default created on the edge nodes, when you create Edge cluster.
- requires uplink to external networks
- deployed only on Edge nodes
- DR and SR are automatically interconnected through transit link