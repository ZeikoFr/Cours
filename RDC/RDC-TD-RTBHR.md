# Rapport TD RTBHR - Gwendal AUPEE

## Démarrage

Création des scripts 1.sh et 2.sh qui seront les routeurs cisco

On se connecte ensuite à chaque switch via un telnet sur la loopback et le port du switch

## Configuration

Une fois les switch up & running, j'ai appliqué la configuration indiquée dans le PDF.

Pour l'installation de nemu j'ai du récupérer le zip directement sur le gitlab car le git clone ne fonctionnait pas.

Une fois nemu installé via le script d'installation il faut préparer le script de lancement des VM via le script fourni dans le PDF et faire le lien symoblique pour accéder à l'image debian.