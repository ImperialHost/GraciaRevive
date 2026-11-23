# `game-api` (Stratul de Contracte 

Reprezintă granița arhitecturală dintre nucleul serverului și logica dinamică a jocului.

## Responsabilități
* Definește interfețele pentru entitățile lumii (`Player`, `Npc`, `Item`).
* Stabilește sistemul de evenimente (*Event Listeners*).
* Definește contractele pentru AI și mecanismele de interacțiune cu quest-urile.

## Beneficii Arhitecturale
* Permite refactorizarea completă a motorului (`game-engine`) fără a afecta scripturile din `game-gameplay`.
* Oferă o decuplare clară între implementarea tehnică și regulile de gameplay.
