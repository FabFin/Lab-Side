# Il framework ICP che ha tagliato il nostro CAC del 42%

*Tempo di lettura: ~9 min*

---

## TL;DR

La maggior parte dei team B2B definisce l'ICP una volta e poi lo ignora. Il risultato: messaggi generici, pipeline inquinata, CAC alle stelle. Il framework "ICP Dinamico" a 3 layer (firmografico + comportamentale + relazionale) ci ha permesso di tagliare il CAC del 42% e raddoppiare il conversion rate in 3 mesi. Template incluso.

---

## Il Problema

Apri il documento "ICP" della tua azienda. Con buona probabilità, trovi qualcosa tipo:

> "SaaS B2B, 50-200 dipendenti, Italia/EU, Series A+, CTO o VP Engineering"

Questo non è un ICP. È una descrizione demografica che potrebbe applicarsi a migliaia di aziende, la maggior parte delle quali non comprerà mai da te.

Il risultato di un ICP così generico:
- **Outbound**: messaggi identici a tutti → response rate < 3%
- **Pipeline**: piena di lead "tiepidi" che non convertiranno mai
- **CAC**: gonfiato perché stai vendendo a chi non ha urgenza
- **Team sales**: frustrato perché "i lead fanno schifo"

Il problema non sono i lead. Il problema è il filtro.

---

## Il Framework: ICP Dinamico a 3 Layer

L'idea è semplice: smetti di definire l'ICP come una fotografia statica e inizia a trattarlo come un modello predittivo a 3 livelli.

```
┌─────────────────────────────────────┐
│  Layer 3: RELAZIONALE               │
│  Warm intro, referral, community    │
├─────────────────────────────────────┤
│  Layer 2: COMPORTAMENTALE           │
│  Intent signal, trigger event       │
├─────────────────────────────────────┤
│  Layer 1: FIRMOGRAFICO              │
│  Settore, dimensione, tech stack    │
└─────────────────────────────────────┘
```

Ogni layer aggiunge un moltiplicatore alla probabilità di conversione. Un lead che matcha tutti e 3 i layer ha 5-8x più probabilità di chiudere rispetto a uno che matcha solo il Layer 1.

---

### Layer 1: Firmografico (il "chi")

Il punto di partenza — necessario ma non sufficiente.

**Attributi**:
- Settore / verticale
- Dimensione (revenue, dipendenti)
- Tech stack (es. usa HubSpot? Salesforce? Tool custom?)
- Stadio (bootstrap, seed, Series A-C)
- Geografia

**Come ricavarlo**: Analizza i tuoi ultimi 20 deal chiusi. Quali pattern emergono? Non guardare solo chi ha comprato — guarda chi ha comprato E rinnovato.

### Layer 2: Comportamentale (il "quando")

Questo layer risponde alla domanda: "Questo lead ha bisogno di noi ADESSO?"

**Segnali di intent**:
- Sta assumendo per ruoli chiave (es. "Head of Sales" su LinkedIn)
- Ha cambiato tech stack di recente
- Ha ricevuto un round di funding negli ultimi 6 mesi
- Sta cercando attivamente soluzioni (G2, Capterra, keyword search)
- Ha interagito con il tuo contenuto (ha aperto 3+ email, ha commentato su LinkedIn)

**Trigger event**:
- Nuovo CTO/VP Sales arrivato (i nuovi leader comprano nei primi 90 giorni)
- Lancio nuovo prodotto
- Espansione in un nuovo mercato
- Competitor ha chiuso/pivotato

**Come tracciarlo**: Clay + LinkedIn Sales Navigator + Google Alerts. Oppure manualmente con una checklist settimanale.

### Layer 3: Relazionale (il "come")

Il layer più sottovalutato e il più potente.

**Attributi**:
- Conosci qualcuno nell'azienda? (warm intro)
- Un tuo cliente li conosce? (referral)
- Sono nella tua community/newsletter?
- Hanno interagito con te in un evento?

**Perché conta**: Un cold outbound a un lead Layer 1+2 converte al 5-10%. Lo stesso lead con un warm intro (Layer 3) converte al 20-30%.

---

## Come Applicarlo — Step by Step

### Step 1: Audit dei deal chiusi (2 ore)

Prendi i deal chiusi negli ultimi 6 mesi. Per ognuno, compila:

| Deal | Settore | Dimensione | Tech Stack | Trigger Event | Warm Intro? | Tempo Ciclo | ACV |
|------|---------|------------|------------|---------------|-------------|-------------|-----|
| ...  | ...     | ...        | ...        | ...           | Sì/No       | ...         | ... |

Cerca i pattern: i deal migliori (alto ACV, ciclo corto, basso churn) cosa hanno in comune?

### Step 2: Definisci lo Score ICP

Assegna un punteggio a ogni attributo:

**Layer 1** (max 30 punti):
- Settore match: 10 pt
- Dimensione match: 10 pt
- Tech stack match: 10 pt

**Layer 2** (max 40 punti):
- Hiring signal: 10 pt
- Funding recente: 10 pt
- Tech stack change: 10 pt
- Content engagement: 10 pt

**Layer 3** (max 30 punti):
- Warm intro disponibile: 15 pt
- Referral da cliente: 15 pt

**Segmentazione**:
- **Tier A** (70-100 pt): Priorità massima. Outbound personalizzato + warm intro.
- **Tier B** (40-69 pt): Outbound mirato. Nurturing attivo.
- **Tier C** (0-39 pt): Solo inbound. Nessun outbound attivo.

### Step 3: Integra nel CRM

- Crea un campo custom "ICP Score" nel CRM
- Imposta un workflow che aggiorna lo score in base ai segnali (Clay o manuale)
- Crea view/report filtrati per Tier
- Il team sales lavora la pipeline dall'alto verso il basso

### Step 4: Review mensile

L'ICP non è un documento statico. Ogni mese:
- Aggiorna i pesi in base ai risultati (cosa converte di più?)
- Aggiungi nuovi segnali che emergono dai deal
- Rimuovi attributi che non predicono la conversione

---

## I Risultati

Abbiamo applicato questo framework su un team di 4 persone (2 AE + 2 SDR), mercato B2B SaaS mid-market.

| Metrica                | Prima       | Dopo (3 mesi) | Variazione |
|------------------------|-------------|---------------|------------|
| CAC                    | €2.800      | €1.624        | **-42%**   |
| Conversion rate (SQL→Deal) | 12%    | 24%           | **+100%**  |
| Tempo medio ciclo      | 45 giorni   | 32 giorni     | -29%       |
| Pipeline Tier A        | N/A         | 35% del totale| —          |
| Response rate outbound | 4%          | 14%           | +250%      |

Il dato più interessante: il **Tier A rappresenta il 35% della pipeline ma genera il 72% del revenue**. Il team ha smesso di perdere tempo sui lead sbagliati.

---

## Template Scaricabile

Ho creato un Google Sheet con:
- Tab 1: Deal Audit (analisi deal chiusi)
- Tab 2: ICP Scoring Matrix (con formule automatiche)
- Tab 3: Segmentazione Tier (A/B/C con azioni consigliate)
- Tab 4: Review Mensile (tracker per aggiornare i pesi)

**Scaricalo qui** → [link in arrivo — rispondi "ICP template" per riceverlo in anteprima]

---

## 3 Errori da Evitare

1. **Definire l'ICP in sala riunioni senza dati**: L'ICP si costruisce dai deal chiusi, non dalle opinioni del founder. Usa i dati, non l'intuito.

2. **Ignorare il Layer 3 (relazionale)**: Il warm intro è il moltiplicatore più potente. Mappare le relazioni è noioso ma cambia i numeri radicalmente.

3. **Non aggiornare mai**: Un ICP vecchio di 6 mesi è un ICP sbagliato. Il mercato cambia, i tuoi clienti cambiano. Review mensile obbligatoria.

---

## La Tua Mossa

Questa settimana, fai una cosa sola: prendi i tuoi ultimi 10 deal chiusi e compila la tabella dello Step 1. In 2 ore avrai più insight sul tuo ICP di quanti ne hai accumulati in mesi di "intuito".

**Rispondi a questa email con i tuoi risultati** — li commento personalmente.

---

*Questo playbook ti ha dato un'idea? Inoltralo al tuo Head of Sales. Costa zero, potrebbe valere un taglio del 40% sul CAC.*

---

*Prossima settimana su Lab Side: "Da €50k a €500k ARR senza un euro in paid" — un case study dal campo con tutti i numeri.*
