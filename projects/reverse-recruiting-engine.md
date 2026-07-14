# Reverse Recruiting Engine

> **TL;DR:** Il recruiting per ruoli senior è una trattativa B2B, non una lotteria ATS.
> Tool con 10 moduli (sourcing, ATS scanner, outreach, negoziazione, CRM personale)
> per gestire la propria ricerca di lavoro come una sales pipeline.

**Status:** In sviluppo — beta privata, backend multi-utente in corso.
**Repo:** [FabFin/My-bio](https://github.com/FabFin/My-bio/tree/main/reverse-recruiting-app)

---

## Cos'è

Il progetto ha due livelli:

1. **Reverse Recruiting Engine** (`reverse-recruiting-engine/`) — il sistema
   di outreach automatizzato (Apollo + Clay + Airtable + n8n) usato in prima
   persona da Fabrizio per la propria ricerca di ruolo Head of Sales.
2. **Reverse Recruiting App** (`reverse-recruiting-app/`) — la web app
   (React/TypeScript, sviluppata con Antigravity) che porta la stessa
   metodologia ad altri candidati senior, in beta privata via invito:
   Posizionamento, ATS Scanner, Radar annunci, Cover Letter AI, Outreach
   Generator, Interview Simulator, Negotiation Script, Pipeline CRM,
   Automazione, Content/Personal Branding.

## Il backend (nuovo)

L'app era client-only (dati in LocalStorage, chiamate dirette alle API AI
dal browser) — non mettibile in produzione multi-utente senza esporre le
chiavi API. `reverse-recruiting-app/backend/` aggiunge:

- Login con **codice invito** (Supabase Auth)
- **Quota mensile di chiamate API** per utente, per limitare l'accesso beta
- **Proxy autenticato** verso Claude e Apify — le chiavi restano sul server

Dettagli tecnici e setup: [`reverse-recruiting-app/backend/README.md`](https://github.com/FabFin/My-bio/blob/main/reverse-recruiting-app/backend/README.md).

## Prossimi passi

- [ ] Portare il codice frontend Antigravity in questo repo
- [ ] Collegare login + moduli AI al backend
- [ ] Deploy backend su Supabase + dominio `reverserecruiting.fabriziofinucci.com`
- [ ] Valutare monetizzazione oltre la beta gratuita a inviti (Stripe)

---

**Tags:** GTM · AI · Recruiting · Sales Pipeline · Lab
