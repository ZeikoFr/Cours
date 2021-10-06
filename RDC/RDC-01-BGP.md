# BGP

- Rappel sur les protocoles IPv4 et v6 et tables de routage en AS
- OSPF est un protocole dispo uniquement dans un AS
- Afin de contacter un autre AS il faut utiliser un protocole "internet" tel que BGP qui est un protocole dynamique.
- Utilise TCP pour envoyer les messages de routage (OSPF lui utilisait directement la couche IP)
- Data Plain = traffic de data
- Control plain = traffic de controle sur le réseau

| L2 | IP | TCP | BGP |

- BGP a pour but de trouver tous les chemins possibles. Vu que l'interieur d'un AS n'est pas révélé trouver un chemin optimal est impossible.

Pour chaque AS BGP distingue :

|                 |                                          |
|-----------------|------------------------------------------|
| local traffic   | traffic with source or destination in AS |
| transit traffic |                                          |
|                 |                                          |
|                 |                                          |
|                 |                                          |

Chaque AS a :

- Un BGP speaker qui annonce :
    - A remplir

## BGP terminology

- Neighbor
    - Configured BGP peer
- NLRI/prefix
    - Reachable information for a IP address & netmask
- Router-ID
- Route/path
    - Chemin vers le voisin 

## Protocol basics 

### Types de messages
   
- Open
- Update
- KeepAlive
- Notification

### Basic operation of BGP

- Each AS as a set of NLRI
- NLRI are exchanged between users

## BGPpeers

- Les BGP speakers sont appelés Peers
- Les speakers qui sont dans différents AS sont des peer externes

- Les interfaces de loopback sont utilisée en tant que peer-connection endpoint

### BGP peers exchange

### BGP attributes

- Les routes apprisent via BGP ont des propriétés associées utilisée pour déterminer la meilleure routes.
    - Origin
    - AS Path
    - Next hop
    - Local preference
    - Multi-Exit discriminator
    - Community

### BGP Updates

- Si un réseau n'est plus disponible une requête de withdraw est envoyée

### BGP routing information base (RIB)

- BGP 'aggregate-addresse' permet de faire de l'agregation d'adresses et de réduire la table de routage
- BGP 'redistribute' peux être utiliser pour remplir le BGP RIB avec les routes de la table de routage

### BGP "IN" process

- Réception d'information de chemin a partir des peers

### BGP "OUT" process

- Construction d'un message se basant sur la RIB
- Envoi du message au peer voisin en s'indiquant soi-même en tant que Next-hop

Une fois les process IN et OUT fait on installe les routes dans la FIB (avec le hop le plus faible)

### Selection des routes

1) Chemin d'AS le plus court
2) Origine la plus faible IGP < EGP < INCOMPLETE
3) Lowest MED 
4) External over internal : route la plus proche du noeud de sortie
5) Closest next-hop : La sortie la plus proche pour un AS donné
6) Lowest router-id

### BGP Issues

- Scalability : Un routeur backbone doit être capable de forward tout paquets quelques que soit sa destination sur internet.
- Nature autonome des domaines
- Problèmes de confiance dans les systèmes autonomes voisins

## AS Path

- Sequences d'AS qu'une route a traversée
- Détection des boucles
- Applications des règles

### AS-path loop detection



#### Pq avons nous besoins d'un protocole de routage externe

- Scaling to large network
- Permet de gérer une hiérarchie
- Limite les impacts des incidents
- Permet une gestion administrative des frontières du réseau de l'AS

#### Policy 

- Controller l'accès à chaque préfixe
- Pas supporter par les IRP

#### Performance

- Intra-AS : gérer la performance
- Inter-AS : La politique peut gouverner au dessus de la performance.


## AS

- Identifié par son AS number
- Il existe des numéros public et privé d'AS

### Terminologie

- Packet flow : data et info utilisateurs
- Routing flow : Message dédiés au tables de routage
- egress = Sortie ingress = Entrée

Le routing flow est nécessaire pour le packet flow

### Egress traffic : traffic sortant du réseau

Basé sur :

- La disponibilité des routes que possède l'AS sortant
- L'acceptation des routes chez les autres AS
- Policy et tuning (que faire des routes que les autres m'ont fournis)
- Peering et transit agreement

### Ingress traffic

Basé sur :

- Les annoncés qu'on a envoyées et a qui ont les a envoyées

### Types de routes

- Static
- Connectées : Créée automatiquement quand une interface est up
- Intérieure : Route interne dans un AS
- Externe : Route externe à un AS

### Longest prefix matching

On prend tjrs le prefixe le plus long lors d'un choix de route (/24 sera choisi au dessus du /16)

