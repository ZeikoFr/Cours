# Rapport TD HackRF - Gwendal AUPEE

##  Résumé du TD

Le but de ce TD était de réussir via l'outil **GNU Radion Companion** à réceptionner la radio sur notre poste en utilisant une antenne **HackRF ONE**

###  Présentation des outils

- **GNU Radio Companion**  
    Logiciel Open-Source fournissant un affichage graphique à GNU Radio pour créer et utilisé de la radio logiciel ou juste de la gestion de signaux. Utilisable dans de nombreux cas d'usage (recherche, hobby, commercial) fourni sous licence GPL 3
- **HackRF ONE**  
    Software Defined Radio (SDR) crée et produit par Great Scott Gadgets, Open source et Open Hardware
    
####  Déroulement du TD

Via **GNURC** et en suivant le pdf fourni, j'ai crée différents blocs avec pour chaque des paramètres spécifique à leur fonctionnement.  
Une fois l'ensemble des blocs connectés et configurés il est possible de capter un signal radio via l'antenne du **HackRF**.

Chaque bloc représente un composant physique d'une radio classique, l'idée étant de comprendre l'imbrication de chaque bloc et de réussir à faire communiquer l'ensemble du pipeline allant de la source à la sortie audio.

**GNURC** se charge de la compilation de l'ensemble des blocs et produits 2 fichiers, un XML et un python.

Le XML contient les valeurs de chaque variables pour la gestion générale du projet (sauvegarde des valeurs et des emplacements des blocs).  
Le python lui est chargé de l'exécution du programme résultant des blocs et des valeurs.  

![Schéma final de fonctionnement](/media/gaupee/37E6CDE3178DBC49/screen.png)

#### Problèmes rencontrés

Les problèmes rencontrés durant ce TD concernait majoritairement des soucis d'incompatibilités entre les versions d'OS et de **GNURC**, certains blocs fournis dans le PDF n'existait plus dans le logiciel et il a donc fallut trouver des alternatives.  

Une fois **GNURC** exécuté directement sur le poste de travail il fut plus simple d'utiliser le **HackRF** avec **GNURC** et progresser plus rapidement dans le TD.  

Les derniers blocages rencontrés concernait les valeurs attribuées à certains variables notamment **Transition width** dans le bloc **Low Pass Filter** en effet cette valeur doit être la plus petite possible et mon réglage initial à 1 Million était trop élevé, j'ai atteint un fonctionnement correct à 100k et également à 10k mais avec un peu plus de difficultés pour capter le signal (qui était fort et clair une fois localisé).  

#### Résultat du TD

J'ai pu réussir à capter différentes radios locales (fréquences fournies dans le PDF) et ainsi atteindre le résultat attendu du TD.  
 Cela m'a permis de mieux comprendre le fonctionnement et la logique de transmission des signaux radios, ainsi que l'importance des canaux et le "faible" écart qui peut être présent entre 2 fréquence d'inforamtion différentes. (L'écart entre 2 stations radios par exemple)

![Affichage du spectre de la fréquence captée](/media/gaupee/37E6CDE3178DBC49/screen2.png)
