# `game-content` (Date Statice / Fostul Datapack)

Reprezintă definițiile declarative ale lumii de joc, complet separate de codul Java compilat.

## Responsabilități
* **Definiții XML:** Statisticile itemelor, armelor, armurilor, skill-urilor și ale NPC-urilor.
* **Lume & Economie:** Tabelele de drop/spoil, liste de spawn-uri, magazine (*multisell*) și zone geografice.
* **Interfață NPC:** Fișiere HTML pentru ferestrele de dialog ale NPC-urilor, teleporterilor și quest-urilor.

## Beneficii Arhitecturale
* Permite modificarea și echilibrarea datelor de joc fără a recompila nucleul Java (`game-engine`).
