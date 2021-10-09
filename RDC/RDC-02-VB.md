# Data Center Networks : Virtual Bridging

## Overview

- VB to connect to VM
- IEEE Virtual Edge Bridging Standard
- Single Root I/O Virtualization (SR-IOV)
- Aggregating Brindges and Links : VSS and vPC
- Bridges with massive number of ports : VBE

## Network Virtualization

1) NV allows tenants to form an overlay network in a multi-tenant network such than tenant can control :
    - Connectivity layer
    - Mac and IP addresses
    - Network Partitions
    - Node Location
2) NV allows providers to serve a large number of tenants without worrying about
    - Internal addresses used in client networks
    - Number of client nodes
    - Location of individual client nodes
    - Number and values of client partitions

### vSwitch

Problem : Multiple VMs on a server need to use one physical NIC  
Solution : Hypervisor creates multiple vNICs connected via a virtual switch (vSwitch)

### Virtual Bridging

*insert screenshot*

VB / VEB / VEPA

### PCIe

- Serial point-to-point interconnect with multiple lanes (PCIe 5 = 4Go/s per lane)

## Combining Bridges

Problems :  

- Number of VM is growing very fast
- Need switches with very large number of ports
- Easy to manage one bridge than 100 10-port bridges
- How to make very large switches ?

Solutions :

1) Distributed Virtual Switch (DVS)
2) Virtual Switching System ()VSS
3) Virtual PortChannels (vPC)
4) Fabric Extension (FEX)
5) Virtual Bridge Port Extension (VBE)

