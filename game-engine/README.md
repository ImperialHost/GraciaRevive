# `game-engine` (Nucleul / Fostul GameServer)

Inima tehnică a proiectului (*Microkernel Core*), organizată intern pe straturi (`Rețea` -> `Servicii` -> `Persistență` -> `Model`).

## Responsabilități
* **Network Layer:** Gestionarea conexiunilor TCP, serializarea/deserializarea pachetelor binare specifice protocolului *Gracia Final* (optimizat cu facilitățile moderne din Java 21, precum *Virtual Threads* și *Records*).
* **World & Combat:** Managementul hărților, regiunilor, vizibilității (*KnownList*), formulelor de luptă, skill-urilor și efectelor.
* **Persistence Layer:** Gestionarea pool-ului de conexiuni și a operațiunilor CRUD către baza de date.

## Arhitectură
* Funcționează ca proces principal al lumii de joc, comunicând securizat cu `auth-service`.
* Expune contractele din `game-api` pentru a încărca dinamic logica din `game-gameplay`.
