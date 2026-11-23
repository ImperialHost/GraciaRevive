<div align="center">
  <img src="../assets/auth-service.jpg" alt="GraciaRevive Auth Service" width="350" />

  <h1>Auth Service</h1>

  <p>
    Serviciul independent pentru autentificarea utilizatorilor și inițializarea sesiunilor de joc.
  </p>
</div>

---

## Responsabilități

- Validarea conturilor și a credențialelor.
- Gestionarea listei serverelor de joc disponibile.
- Generarea cheilor unice de sesiune.
- Securizarea pachetelor de autentificare utilizate în comunicarea cu clienții.

## Arhitectură

- Rulează într-un proces separat de `game-engine`.
- Comunică cu serverele de joc printr-un canal intern securizat.
- Nu gestionează logica de joc sau starea lumii.

