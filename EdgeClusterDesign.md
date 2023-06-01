# Edge Cluster Design considerations

The main considerations are
1. where to place edge nodes
2. when should you use additional edge cluster

## Additional Edge Cluster
The following factors decides when additional cluster is required

1. You wish to dedicate T0 per domain e.g. in workload domain there is single Edge cluster and it continues to be used for additional domain
2. Multi-tenant model
3. Separating routing and service traffic i.e. separate stateful and stateful services
4. Asymmetric bandwidth for T1 versus T0
5. ECMP for T0 & Active-Standby for Tier-1 in a single node. BFD detection fails the entire Edge Node, so If Tier-0 and Tier-1 are mixed, both fails.