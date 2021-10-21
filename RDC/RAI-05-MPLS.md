# MPLS - Multi Protocol Label Switching

## Acronyms

- PE provider edge router
- P Provider core router
- CE CUstomer Edge router
- ASBR Autonomous System Boundary Router
- RR Route Reflector

## AToM - Any Transport over MPLS

- Commonly known scheme for building layer 2 circuits over MPLS

## Label Stacking

- Multiples lables can be put in an MPLS packet


## VPNs

- Layer 2 VPNs
    - Customer end points (CPE) connected via layer 2 or point to point connection
    - Multiple logical connections (one with each end point)
- Layer 3 VPNs
    - Customer end points peer with provider routers
    - Single peering relationship
    - No mesh of connections
    - Provider network responsible for
        - Distributing routing information to VPN sites
        - Separation of routing tables from one VPN to another

