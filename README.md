# 🏋️‍♂️ GymAccess - IoT QR-Code Access Management System

![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=for-the-badge&logo=spring-boot&logoColor=white)
![Angular](https://img.shields.io/badge/Angular-DD0031?style=for-the-badge&logo=angular&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
🏋️‍♂️ GymAccess - IoT & SaaS Access Management System
Sistema Full-Stack e IoT per la gestione degli accessi fisici in ambito fitness tramite Scansione QR Code. Il progetto integra una dashboard gestionale enterprise con un sistema hardware di visione artificiale, supportato da un'infrastruttura Cloud sicura e scalabile.

🎯 L'Obiettivo del Progetto
Dimostrare la capacità di integrare Computer Vision, logiche di business avanzate, sicurezza dei dati sensibili e un'infrastruttura DevOps/Cloud in un unico ecosistema. Il sistema risolve il problema della gestione accessi in modo contactless e paperless, offrendo al contempo strumenti di Business Intelligence e conformità GDPR per il management della palestra.

🏗 Architettura del Sistema & Cloud Infrastructure
Il sistema è strutturato su un'architettura a micro-servizi distribuiti per garantire massima sicurezza e performance:

Hardware / Edge Vision: Una telecamera (gestita tramite script Python e OpenCV) scansiona il QR Code. Il payload viene inviato al backend. In caso di validazione (HTTP 200), il sistema sblocca il tornello fisico.

Frontend (Cloudflare Pages): Single Page Application (SPA) in Angular distribuita su CDN globale per garantire caricamenti fulminei e latenza minima.

Backend Server (DigitalOcean Droplet): Il "cervello" in Spring Boot 3. Valida le logiche di business, autentica gli utenti (JWT) e fa da scudo verso i dati.

Database Isolato (DigitalOcean VPC): PostgreSQL è ospitato su un Droplet separato e inserito in una Virtual Private Cloud (VPC). Nessuna porta è esposta su internet: accetta connessioni esclusivamente dal Droplet di backend, garantendo una sicurezza dei dati di livello bancario.

✨ Core Features & Ingegneria del Software
Sicurezza Documentale (Zero-Trust): I file sensibili (come i certificati medici in PDF) non sono esposti tramite link diretti (href). Il download avviene tramite chiamate HTTP autenticate con JWT che restituiscono un flusso di byte (Blob), generando link temporanei invisibili ai malintenzionati.

Reattività Estrema (Angular Signals): Il frontend sfrutta i Signal di Angular 17+ per l'aggiornamento reattivo dello stato locale. Le operazioni CRUD (es. aggiunta/modifica allievi) aggiornano la UI istantaneamente in RAM, abbattendo le chiamate API ridondanti e migliorando la UX.

Ottimizzazione DB (Layer di Caching): Implementazione di Caffeine Cache in-memory sul backend per la Dashboard Analytics. Le statistiche complesse e le query di aggregazione vengono salvate in RAM, riducendo drasticamente il carico su PostgreSQL.

GDPR Compliance & Portabilità: Sviluppo di un sistema per l'esportazione dinamica dei dati degli allievi in formato strutturato (CSV), garantendo il rispetto dell'Articolo 20 del GDPR (Diritto alla portabilità dei dati).

Gestione Dinamica Abbonamenti e Certificati:

Pattern State/Enum in Java per differenziare abbonamenti a tempo e a ingressi.

Sistema visuale a "semaforo" (tramite Tag UI) per monitorare e bloccare preventivamente gli accessi con certificati medici scaduti.

Transazioni Atomiche: Utilizzo di @Transactional per garantire l'integrità dei database: l'ingresso viene scalato e la presenza registrata simultaneamente, o si attiva il rollback.

🛠 Stack Tecnologico e Scelte Progettuali
Backend & Sicurezza
Java 17+ & Spring Boot 3: Affidabilità e standardizzazione enterprise.

Spring Security & JWT: Autenticazione stateless e autorizzazione per endpoint sensibili.

Caffeine Cache: Layer di caching In-Memory locale per performance in lettura a latenza zero.

Database
PostgreSQL: Robusto sistema RDBMS relazionale.

Frontend
Angular 17+: Architettura a componenti e gestione reattiva avanzata (Signals).

PrimeNG & TailwindCSS/PrimeFlex: UI components di alto livello (Tabelle dinamiche, ConfirmDialog, Toast, Forms) per un design pulito, responsive e professionale.

DevOps & IoT
DigitalOcean & Cloudflare: Hosting multi-nodo con separazione fisica tra Applicativo e Database (VPC).

Python & OpenCV: Script lato camera per il rilevamento ottico.

💡 Lezioni Apprese
Durante lo sviluppo ho consolidato principi di software engineering avanzati:

Sicurezza Oltre il Login: Ho imparato che la vera sicurezza non si ferma al login, ma si estende all'architettura di rete (VPC) e alla gestione in memoria dei file sensibili (Blob/Streams).

Gestione delle Risorse: Progettare pensando alla scalabilità, scegliendo strumenti come Caffeine Cache per ottimizzare un'architettura single-node senza introdurre over-engineering non necessario (come cluster Redis prematuri).

Data Integrity: Gestione sicura di date, timezones e concorrenza per evitare falle negli accessi fisici (Anti-Passback) e validazioni temporali rigorose per abbonamenti e certificati.
