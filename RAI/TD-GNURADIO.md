# Rapport TD GNURADIO - Gwendal AUPEE

## Déroulement du TD

## Réponses au questions

- Q1 : La charge CPU est très importante sans block throttle

    *inset screenshot Q1*
    
    Une fois le bloc mit en place la consommation CPU baisse énormément  
    *inset Q1b*
    
- Q2 : Il y a deux courbe car il y a la phase et la quadrature de phase à 90° de la phase  
- Q3 : La forme de la courbe change il n'y a plus qu'une courbe au lieu de 2  
- Q5a : La random source à une sortie en Short que ne peut pas traiter correctement le GUI sink, il faut donc un convertisseur short to float afin de permettra un lancement du schéma.  
- Q7 : En augmentant l'amplitude le signal à une forme très différente.  
*insert Q7*

- Q9 : Le slider permet de modifier en direct la fréquence source, chaque modification a un impact sur la forme de la courbe dans le Scope Sink et dans le FFT Sink, la répartition au niveau de l'historique (Histo sink) reste la même quelle que soit la fréquence.
- Q10 : Quand la fréquence de la sinusoïde dépasse les 15kHz le pic présent sur le graph FFT revient sur les fréquences plus basse c'est du à la formule suivante : A $\sin(\frac{2\pi}{T}t+\theta)$ 

- Q12 : On peut voir sur le FFT plot la présence de la fréquence 4kHz, je n'ai pas déduit grand chose du scope plot