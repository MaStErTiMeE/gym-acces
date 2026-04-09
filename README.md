# 🏋️‍♂️ GymAccess - IoT QR-Code Access Management System

![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=for-the-badge&logo=spring-boot&logoColor=white)
![Angular](https://img.shields.io/badge/Angular-DD0031?style=for-the-badge&logo=angular&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)

Sistema Full-Stack e IoT per la gestione degli accessi fisici in ambito fitness tramite **Scansione QR Code**. Il progetto integra una dashboard gestionale enterprise con un sistema hardware di visione artificiale per l'automazione del controllo accessi in tempo reale.

## 🎯 L'Obiettivo del Progetto
Dimostrare la capacità di integrare **Computer Vision**, logiche di business avanzate e un'infrastruttura DevOps in un unico ecosistema scalabile, risolvendo il problema della gestione accessi in modo contactless e paperless.

---

## 🏗 Architettura del Sistema

Il sistema è suddiviso in tre macro-livelli interconnessi:

1. **Hardware / Computer Vision:** Una telecamera (gestita tramite script Python e OpenCV) scansiona il QR Code dell'utente. Il payload decodificato viene inviato come identificativo univoco alle API REST del backend. In caso di codice HTTP 200 (OK), il sistema sblocca il tornello.
2. **Backend (Spring Boot):** Il "cervello" dell'applicativo. Valida l'identificativo, verifica le regole di business (stato dell'abbonamento, tipologia, ingressi residui) ed elabora la transazione sul database.
3. **Frontend (Angular):** Dashboard per l'amministrazione, che permette di gestire le anagrafiche, monitorare lo storico accessi e generare i QR Code per gli iscritti.

## ✨ Core Features & Logica di Business

* **Validazione Contactless:** Accesso tramite scansione ottica, pronto per l'integrazione con eventuali App Mobile.
* **Gestione Dinamica Abbonamenti:** Utilizzo del pattern State/Enum in Java per differenziare automaticamente l'elaborazione tra abbonamenti a scadenza temporale (es. Mensile/Annuale) e pacchetti a scalare (es. 10 Ingressi).
* **Transazioni Atomiche:** Sfruttamento di `@Transactional` per garantire la totale integrità dei dati (l'ingresso viene scalato e la presenza registrata simultaneamente, oppure l'intera operazione subisce un rollback in caso di errore).
* **Infrastruttura Professionale:** Applicazione multi-tier containerizzata e progettata per operare dietro a un Reverse Proxy protetto.

---

## 🛠 Stack Tecnologico e Scelte Progettuali

### Backend & Integrazione IoT
* **Java 17+ & Spring Boot 3:** Scelti per l'affidabilità, la sicurezza e la standardizzazione in contesti enterprise.
* **Spring Data JPA / Hibernate:** Livello ORM per l'interazione efficiente e sicura con la persistenza dei dati.
* **Python & OpenCV:** Script lato camera periferica per il rilevamento e la decodifica dei codici ottici a bassissima latenza.

### Database
* **PostgreSQL:** Scelto come database relazionale primario al posto del tradizionale MySQL per la sua superiore aderenza agli standard SQL, la robustezza ACID e le eccellenti performance con architetture containerizzate.

### Frontend
* **Angular:** Framework robusto per la creazione di una Single Page Application (SPA) modulare.
* **UI Framework:** Interfaccia gestionale progettata per la massima usabilità, concentrata su flussi operativi rapidi e dati tabellari puliti.

### DevOps & Infrastruttura
* **Docker & Docker-Compose:** Tutti i servizi (Backend, Frontend, DB) sono orchestrati in container isolati.
* **Reverse Proxy & DNS:** Il traffico è gestito tramite proxy (Nginx/Traefik) per centralizzare la sicurezza, i certificati SSL/HTTPS e il bilanciamento.

---

## 💡 Lezioni Apprese
Durante lo sviluppo ho consolidato principi di software engineering fondamentali:
- **Separation of Concerns:** Divisione netta tra API Routing (`Controller`), regole architetturali (`Service`) e interazione dati (`Repository`).
- **Data Integrity:** Gestione sicura di date, timezones e concorrenza per evitare falle negli accessi (es. ingressi multipli simultanei).
- **System Integration:** Far comunicare in modo affidabile uno script locale di Computer Vision con API Java remote, gestendo e interpretando correttamente i vari status code HTTP.

---

## 🚀 Setup e Installazione (Ambiente Locale)

1. Clona il repository:
   ```bash
   git clone [https://github.com/](https://github.com/)[TUO-NOME-UTENTE]/gym-access-system.git
