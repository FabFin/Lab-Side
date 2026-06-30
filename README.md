# Lab-Side — GTM × AI Automation

> Esperimenti reali su come l'AI cambia il lavoro di chi fa sales e business development.

**Substack:** [substack.com/@labside](https://substack.com/@labside)  
**Autore:** [Fabrizio Finucci](https://linkedin.com/in/finucci) — Head of Sales | GTM | AI-native

---

## Cosa trovi qui

Questo repo è la base operativa del progetto Lab-Side:
- **`/posts`** — bozze e versioni finali degli articoli Substack (markdown)
- **`/projects`** — documentazione sintetica dei Lab R&D projects attivi
- **`/templates`** — template riutilizzabili per post e analisi

---

## Lab R&D Projects attivi

| Progetto | Repo | Status | Impatto |
|----------|------|--------|---------|
| AIGenBot | [FabFin/AIGenBot](https://github.com/FabFin/AIGenBot) | Attivo | +15% accuracy lead scoring, -50% tempo email, -€0.30/email |
| GTM Automation Framework | [FabFin/gtm-automation-framework](https://github.com/FabFin/gtm-automation-framework) | In aggiornamento | +133% conversion |
| Sales Data Dashboard | [FabFin/sales-data-dashboard](https://github.com/FabFin/sales-data-dashboard) | v2 in arrivo | 15+ metriche real-time |
| Reverse Recruiting Engine | [FabFin/My-bio](https://github.com/FabFin/My-bio/tree/main/reverse-recruiting-engine) | In sviluppo | 4 agenti AI per prospecting |

---

## Come funziona il flusso contenuti

```
idea / esperimento
      ↓
draft in /posts (markdown)
      ↓
revisione + approvazione manuale
      ↓
publish su @labside Substack
      ↓
cross-post su LinkedIn (formato ridotto)
```

---

## Stack

- Claude API (Sonnet) — generazione e analisi
- n8n / Make.com — automazione workflow
- Apollo.io + Clay — data enrichment
- Next.js — sito portfolio [fabriziofinucci.com](https://fabriziofinucci.com)
