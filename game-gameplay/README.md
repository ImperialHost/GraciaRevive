# `game-gameplay` (Plugin-uri / Fostele Scripts)

Conține regulile specifice și comportamentul dinamic al cronicii *Gracia Final*.

## Responsabilități
* Implementarea quest-urilor și a poveștii jocului.
* Comportamentul avansat (AI) al monștrilor și al Raid Boss-ilor.
* Gestionarea instanțelor (ex. *Kamaloka*, *Seed of Destruction*).
* Evenimentele automate și zonele speciale ale lumii.

## Arhitectură
* Funcționează ca un set de plugin-uri încărcate dinamic de `game-engine`.
* Depinde exclusiv de contractele și interfețele definite în `game-api`.
