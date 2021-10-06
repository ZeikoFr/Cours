# Rapport TD GSM - Gwendal AUPEE


## Résumé du TD

##  Déroulement du TD

- Installation d'une VM Debian 11
- Installation de différents paquets fournis dans le PDF

## Réponses au questions :

Q9 : La commande lance wireshark avec un filtre sur la capture sur le protocole "gsmtap" et on exclu du filtre le protocole ICMP, le tout sur l'interface loopback

Q12 : Détail des messages reçus :

- (CCCH) (SS)
- (CCCH) (RR) Paging Request Type 1/2 
    - Les paquets PRT 1 contiennent un channel type CCCH ainsi qu'un antenna number et un sub-slot qui varie par paquet.
- System Information Type 1/2/3/4