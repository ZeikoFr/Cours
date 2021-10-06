# Rapport TD BGP - Gwendal AUPEE


## Création des interfaces

Création de l'interface de loopback `interface loopback 1`

Ajout des adresses IP demandées sur chaque interface :  
`config`  
`interface <InterfaceName>`  
`ip address <IP> <MASK>`

| ROUTEUR | INTERFACE | IP         |
|---------|-----------|------------|
| R1      | LO        | 11.0.0.1/8 |
| R1      | S1/0      | 12.0.0.1/8 |
| R2      | S1/0      | 12.0.0.2/8 |
| R2      | S1/1      | 23.0.0.1/8 |
| R3      | S1/0      | 23.0.0.2/8 |
| R3      | S1/1      | 34.0.0.1/8 |
| R4      | S1/0      | 34.0.0.2/8 |
| R4      | LO        | 44.0.0.1/8 |


Une fois le projet sauvegardé vérification des routes avec la commande `show ip route`

## Configuration BGP

Je configure d'abord le BGP sur chaque routeur :

R1 : config router bgp 1  
R2/R3 : config router bgp 2  
R4 : config router bgp 3  

Je configure les voisins :

R1 : `(config-router) neighbor 12.0.0.2 remote-as 2`  
R2 : `(config-router) neighbor 12.0.0.1 remote-as 1`  
R3 : `(config-router) neighbor 34.0.0.2 remote-as 3`  
R4 : `(config-router) neighbor 34.0.0.1 remote-as 2`  

Afin de permettre à R1 et R4 de communiquer je dois indiquer a R2 et R3 qu'il sont neighbor :

R2 : `(config-router) neighbor 23.0.0.2 remote-as 2`  
R3 : `(config-router) neighbor 23.0.0.1 remote-as 2`  


J'exporte les voisins : `(config-router) network <IP>` sur R1 et 4 uniquement (car ils ont les LO)

Au niveau des tables de routage, chaque routeur indique quels sont les réseaux auquel il est directement connecté et quels sont les peers qui permettent un accès au réseaux suivant

## Réseau avec chemins multiples

Création des interfaces loopback sur R1 3 5 et 7 : `interface loopback 1`

Pour aller plus vite dans les attributions IP les conf ont été fait directement dans les fichiers de conf de chaque routeur.

| ROUTEUR | INTERFACE | IP       |
|---------|-----------|----------|
| R1      | S1/0      | 12.0.0.1 |
| R1      | S1/1      | 18.0.0.1 |
| R1      | LO        | 11.0.0.1 |
| R2      | S1/0      | 12.0.0.2 |
| R2      | S1/1      | 23.0.0.1 |
| R3      | S1/0      | 23.0.0.2 |
| R3      | S1/1      | 34.0.0.1 |
| R3      | LO        | 33.0.0.1 |
| R4      | S1/0      | 34.0.0.2 |
| R4      | S1/1      | 45.0.0.1 |
| R5      | S1/0      | 45.0.0.2 |
| R5      | S1/1      | 56.0.0.1 |
| R5      | LO        | 55.0.0.1 |
| R6      | S1/0      | 56.0.0.2 |
| R6      | S1/1      | 67.0.0.1 |
| R6      | S1/2      | 68.0.0.1 |
| R7      | S1/0      | 67.0.0.2 |
| R7      | S1/1      | 78.0.0.1 |
| R7      | LO        | 77.0.0.1 |
| R8      | S1/0      | 68.0.0.1 |
| R8      | S1/1      | 78.0.0.2 |
| R8      | S1/2      | 18.0.0.2 |


### Configuration RIP & OSPF

Configuration de RIP dans l'AS 2 (R2/3/4)
```
config
router rip
version 2
```

Dans R2 : `network 23.0.0.0`  
Dans R3 : `network 23.0.0.0` `network 34.0.0.0`  
Dans R4 : `network 34.0.0.0`  

Configuration de l'OSPF dans l'AS 4 (R6/7/8)
```
config
router ospf 100
network <IP> 0.0.0.255 area 0
```

Dans R6 : `network 67.0.0.0 0.0.0.255 area 0` `network 68.0.0.0 0.0.0.255 area 0`  
Dans R7 : `network 67.0.0.0 0.0.0.255 area 0` `network 78.0.0.0 0.0.0.255 area 0`  
Dans R8 : `network 68.0.0.0 0.0.0.255 area 0` `network 78.0.0.0 0.0.0.255 area 0`  

### Configuration BGP

Je commence par configurer BGP sur les routeurs de bordure :

R1 : config router bgp 1  
R2 : config router bgp 2  
R4 : config router bgp 2  
R5: config router bgp 3  
R6 : config router bgp 4  
R8 : config router bgp 4  

Configuration des voisins :  

R1 : `(config-router) neighbor 12.0.0.2 remote-as 2` `(config-router) neighbor 18.0.0.2 remote-as 4`  
R2 : `(config-router) neighbor 12.0.0.1 remote-as 1`  
R4 : `(config-router) neighbor 45.0.0.2 remote-as 3`  
R6 : `(config-router) neighbor 45.0.0.1 remote-as 2` `(config-router) neighbor 68.0.0.2 remote-as 4`  
R8 :

### Redistribution

Afin de permettre à l'ensemble des routeurs de communiquer entre eux il faut redistribuer les réseaux BGP dans les RIP et OSPF et inversement.

Redistribution OSPF vers BGP :

Dans R6 et R8 :

```
router bgp 4
redistribute ospf 100 metric 4
```

Redistribution BGP vers OSPF

```
router ospf 100
redistribute bgp 4 subnets
```

# Questions

Question 11 : 

- Les types de paquets échangés sont des paquets HDLC utilisant le protocole SLARP

Q 22 :

- Une fois les redistributions mises en place il faut annoncer sur le BGP les réseaux de bordures des routeur afin que les routeurs présent en interne (R7 et R3) puissent atteindre ces réseaux.

Q 24 :

- Selon le traceroute le paquet passe par l'AS 4 en faisant le chemin suivnat :
    - R1 => R8 => R6 => R5s

Q 25 :

- Une fois le lien coupé il faut attendre quelques secondes pour que les updates BGP soit arrivée à tous les routeurs, le nouveaux chemin devient le suivant :
    - R1 => R2 => R3 => R4 => R5

Q 26:

- Le chemin choisi par R1 pour atteindre P55 ne change pas car nous avons coupé le seul lien de redistribution BGP de l'AS 4, cela oblige R1 à faire tout le chemin de l'AS 2 et 3 pour atteindre le R7 de l'AS4.

Q 27:

- Un message BGP update circule en indiquant qu'il faut supprimer la route 55.0.0.0/8