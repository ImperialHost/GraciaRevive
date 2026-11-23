# `game-registry` (Utilitar CLI de Administrare / Fostul RegisterGameServer)

Aplicație CLI (*Command-Line Interface*) de sine stătătoare, dezvoltată în **Java 21**, destinată administratorului de sistem pentru înregistrarea și gestionarea ciclului de viață al instanțelor de `game-engine` în infrastructura de autentificare.

## Responsabilități
* **Securitate Criptografică:** Generarea de identități unice pe **256 de biți (32 bytes)** folosind CSPRNG (`SecureRandom` + `HexFormat`), salvate în baza de date (`VARBINARY(32)`) și exportate în `hexid/hexid.txt`.
* **Management Servere:** Alocarea ID-urilor predefinite de server (`servername.json`), inițializarea automată a schemei SQL, listarea și revocarea serverelor înregistrate.
* **Compatibilitate & UX:** Suport nativ multi-dialect (**MariaDB** și **MySQL**) cu detecție automată la pornire și interfață bilingvă (`EN` / `RO`).

## Arhitectură și Izolare
* Funcționează complet independent de procesele de producție (`auth-service` și `game-engine`).
* Dispune de propriul pachet de distribuție executabil (`game-registry.jar`).
