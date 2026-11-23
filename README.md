# GraciaRevive

🚧 **Status:** Pre-Alpha | 💻 **IDE:** Eclipse | ☕ **Java:** 21 | 🗄️ **DB:** MariaDB / MySQL | ⚖️ **License:** GPLv3

[![Status](https://shields.io)](https://github.com)
[![IDE](https://shields.io)](https://eclipseide.org)
[![Java](https://shields.io)](https://openjdk.org)
[![MariaDB](https://shields.io)](https://mariadb.org)
[![MySQL](https://shields.io)](https://mysql.com)
[![License: GPL v3](https://shields.io)](https://gnu.org)

Emulator modern și modular pentru **Lineage II: Gracia Final**, construit pe o arhitectură decuplată (*Microkernel Core*) și optimizat cu facilitățile din **Java 21**.

---

## 1. Structura Proiectului (Monorepo)

| Modul / Serviciu | Rol în Ecosistem | Echivalent L2J Clasic |
| :--- | :--- | :--- |
| [`auth-service`](./auth-service) | Serviciu independent de autentificare și sesiuni | `LoginServer` |
| [`game-api`](./game-api) | Stratul de contracte, interfețe și SDK | *N/A (Arhitectură nouă)* |
| [`game-engine`](./game-engine) | Nucleul serverului (*Microkernel Core*, rețea, combat) | `GameServer` |
| [`game-gameplay`](./game-gameplay) | Plugin-uri dinamice (quest-uri, AI, instanțe) | `Scripts` |
| [`game-content`](./game-content) | Date declarative statice (XML / HTML) | `Datapack` |
| [`game-registry`](./game-registry) | Utilitar CLI de administrare și înregistrare servere | `RegisterGameServer` |
| [`database`](./database) | Scheme SQL, date inițiale și migrări | `SQL / Tools` |

---

## 2. Descrierea Modulelor

### 2.1. `auth-service` (Fostul LoginServer)
Serviciu independent responsabil exclusiv cu autentificarea utilizatorilor și gestionarea sesiunilor inițiale.
* **Responsabilități:** Verificarea credențialelor, criptarea pachetelor de login, gestionarea listei de servere de joc disponibile și generarea cheilor de sesiune (`SessionKey`).
* **Izolare:** Rulează într-un proces separat față de `game-engine` și comunică cu acesta printr-un canal intern securizat.

### 2.2. `game-api` (Stratul de Contracte / SDK)
Reprezintă granița arhitecturală dintre nucleul serverului și logica dinamică a jocului.
* **Responsabilități:** Definește interfețele pentru entitățile lumii (`Player`, `Npc`, `Item`), sistemul de evenimente (*Event Listeners*), contractele pentru AI și mecanismele de interacțiune cu quest-urile.
* **Beneficiu:** Permite refactorizarea completă a motorului (`game-engine`) fără a afecta scripturile din `game-gameplay`.

### 2.3. `game-engine` (Nucleul / Fostul GameServer)
Inima tehnică a proiectului (*Microkernel Core*), organizată intern pe straturi (`Rețea` -> `Servicii` -> `Persistență` -> `Model`).
* **Responsabilități:**
  * **Network Layer:** Gestionarea conexiunilor TCP, serializarea/deserializarea pachetelor binare specifice protocolului *Gracia Final* (optimizat cu facilitățile moderne din Java 21, precum *Virtual Threads* și *Records*).
  * **World & Combat:** Managementul hărților, regiunilor, vizibilității (*KnownList*), formulelor de luptă, skill-urilor și efectelor.
  * **Persistence Layer:** Gestionarea pool-ului de conexiuni și a operațiunilor CRUD către baza de date.

### 2.4. `game-gameplay` (Plugin-uri / Fostele Scripts)
Conține regulile specifice și comportamentul dinamic al cronicii *Gracia Final*.
* **Responsabilități:** Implementarea quest-urilor, comportamentul avansat (AI) al monștrilor și al Raid Boss-ilor, instanțele (ex. *Kamaloka*, *Seed of Destruction*), evenimentele automate și zonele speciale.
* **Arhitectură:** Funcționează ca un set de plugin-uri încărcate de `game-engine` și legate prin contractele din `game-api`.

### 2.5. `game-content` (Date Statice / Fostul Datapack)
Reprezintă definițiile declarative ale lumii de joc, complet separate de codul Java compilat.
* **Responsabilități:** Fișiere XML pentru statisticile itemelor, skill-urilor, NPC-urilor, tabelelor de drop, spawn-uri și fișiere HTML pentru interfața de dialog a NPC-urilor.

### 2.6. `game-registry` (Utilitar CLI de Administrare / Fostul RegisterGameServer)
Aplicație CLI (*Command-Line Interface*) de sine stătătoare, dezvoltată în **Java 21**, destinată administratorului de sistem pentru înregistrarea și gestionarea ciclului de viață al instanțelor de `game-engine` în infrastructura de autentificare.
* **Responsabilități:**
  * Generarea de identități criptografice unice pe **256 de biți (32 bytes)** folosind CSPRNG (`SecureRandom` + `HexFormat`), salvate în baza de date (`VARBINARY(32)`) și exportate în `hexid/hexid.txt`.
  * Alocarea ID-urilor predefinite de server (`servername.json`), inițializarea automată a schemei SQL, listarea și revocarea serverelor înregistrate.
  * Suport nativ multi-dialect (**MariaDB** și **MySQL**) cu detecție automată la pornire și interfață bilingvă (`EN` / `RO`).
* **Izolare:** Funcționează complet independent de procesele de producție (`auth-service` și `game-engine`), având propriul său pachet de distribuție (`game-registry.jar`).

### 2.7. `database` (Infrastructura de Date)
Conține definiția structurală a bazei de date relaționale.
* **Responsabilități:** Scripturi `.sql` pentru crearea tabelelor, datele statice inițiale, indexarea pentru performanță și scripturile de migrare între versiuni.

---

## 3. Licență

Acest proiect este distribuit sub licența **GNU General Public License v3.0 (GPLv3)**.
