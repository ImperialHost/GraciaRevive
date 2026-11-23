# `auth-service` (Fostul LoginServer)

Serviciu independent responsabil exclusiv cu autentificarea utilizatorilor și gestionarea sesiunilor inițiale.

## Responsabilități
* Verificarea credențialelor și validarea conturilor.
* Criptarea pachetelor de login.
* Gestionarea listei de servere de joc disponibile.
* Generarea cheilor de sesiune (`SessionKey`).

## Arhitectură și Izolare
* Rulează într-un proces separat față de `game-engine`.
* Comunică cu serverele de joc printr-un canal intern securizat.
