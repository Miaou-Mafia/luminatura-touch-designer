# Luminatura projection (Touch Designer)

## Pure Data - Touch Designer

Les données brutes sont transmises à TouchDesigner pour modifier la projection visuelle.
Lorsque l’utilisateur pose sa main sur la plaque, le visuel s’intensifie, renforçant l’immersion dans l'expérience interactive.
À l’inverse, lorsque la main est retirée, les effets visuels s’atténuent progressivement, accompagnant la fin du son et des lumières.

| Port  | Fonction                              |
| ----- | ------------------------------------- |
| 10002 | TouchDesigner - projection sur le sol |
| 10004 | TouchDesigner - projection sur le mur |

Effets visuels pour toutes les plaques
* Projection du mur
    * Deux des 6 particles GPU passent de 10 particules à 500 quand une des plaques est touchée.
    * Le gamma devient de plus en plus fort quand les surfaces des mains augmentent
    * Toutes les particles GPU passent au mauve quand la plaque 1 et la plaque 2 sont activées
    * Toutes les particles GPU passent au vert quand la plaque 2 et la plaque 3 sont activées
    * Toutes les particles GPU passent au rouge quand la plaque 1 et la plaque 3 sont activées
    * Toutes les particles GPU changent de couleur (mauve, vert, rouge, rose, bleu, jaune) en interval quand toutes les plaques sont activées
    * Quand toutes les plaques sont activées, le vent du particles GPU se mets en mouvement grâce à des LFOs

Effets visuels pour la plaque 1
* Projection du sol
    * Le particles GPU passe d'une force qui se focus au centre à une force qui se focus vers la plaque 1 (centre)
      
* Projection du mur
    * Toutes les particles GPU passent au rose quand la plaque 1 est activée

Effets visuels pour la plaque 2
* Projection du sol
    * Le particles GPU passe d'une force qui se focus au centre à une force qui se focus vers la plaque 2 (gauche)
      
* Projection du mur
    * Toutes les particles GPU passent au bleu quand la plaque 2 est activée

Effets visuels pour la plaque 3
* Projection du sol
    * Le particles GPU passe d'une force qui se focus au centre à une force qui se focus vers la plaque 3 (droite)

* Projection du mur
    * Toutes les particles GPU passent au jaune quand la plaque 3 est activée


## Projection mur

```mermaid
flowchart TD
    subgraph Plafond
        A[Alimentation] --> B[Projecteur du sol 192.168.1.180]
        A --> C[Ampoule 1]
        A --> D[Ampoule 2]
        A --> E[Ampoule 3]
        A --> F[HDMI Extender RX #31]
        F -->| Cable HDMI | B
        G[Ethernet Port 94] -->| Cable Ethernet | B
        H[Ethernet Port 93] -->| Cable Ethernet | F
        A --> I[Projecteur du mur 192.168.1.21]
        K[Ethernet Port 81] -->| Cable Ethernet | I
        L[Ethernet Port 80] -->| Cable Ethernet | M[HDMI Extender RX #15]
        M --> I
        A --> M
    end
```
## Projection sol

```mermaid
flowchart TD
    subgraph Sol
        N[Alimentation] --> O
        O[HDMI Extender TX #31] -->| Cable HDMI | P[Ordinateur 192.168.1.178]
        Q[Ethernet Port 247] -->| Cable Ethernet | O
        N --> R[Speaker]
        R -->| Cable XLR | S[Adaptateur Audio]
        N --> T
        T[Carte de son] --> U[Ordinateur 192.168.1.150]
        N --> V
        V[TP Link] --> | Ethernet Port 219 | Atom
        Atom --> | Tape d'aluminum | X[Plaque en acier]
        Y[ Ethernet Port 253] --> Atom
        V --> | Ethernet Port 218 | Ethernet
        V --> | Cable Ethernet | W[Ordinateur 192.168.1.140]
    end
```
