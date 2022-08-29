# AODV

- Ad-hoc On-Demand Distance Vector Routing
- Construct a route when needed
- Routing table : Path is not stored, only next hop


- Intermediate node can reply to RREQ only if they have a route to dest with higher dest sequence #
- Route Reply come back in unicast on the reverse path
- Backward route to dest is recorded if sequence number is higher or if sequence number is same

## Route maintenance in AODV

- Each node keep a list of active neighbors
- If a link in a routing table breaks all active neighbours are informed by a "route error" messages

# Dynamic Source Routing

- On Demand routing using "Source Route"
- 