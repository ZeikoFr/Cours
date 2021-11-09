# Open flow

## Planes of Networking

- Data plane : All activities involving as well as resulting from data packets sent by the end user.  
    - Forwarding
    - Fragmentation and reassembly
    - Replication for multicasting

- Control plane : All activities that are necessary to perform data plane activities but do not involve end-user data packets  
    - test
    - Making routing tables
    - Setting packet handling policies
    - Base station beacons annoncing availability of services

## Flow table exemple

- Idle timeout : Remove entry if no packets received for this time
- Hard tiemout : Remove entry after this time
- If both are set, the entry is removed if either one expires

## Actions

- Forward to Physical Port i or to Virtual Port
- Enqueue
- Drop
- Modify Field
- lot more....

## Open vSwitch

- Open source virtual switch
