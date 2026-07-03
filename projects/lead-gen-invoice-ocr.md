# Lead Gen — Tool AI di estrazione dati da fatture (OCR)

> Lookalike analysis sui clienti esistenti → lista prospect qualificata per outreach.
> Data: 2026-07-02 · Fonte: Apollo.io (2 ricerche aziende) + ricerca web per profilazione seed.

---

## 1. Seed: i clienti di partenza

| Cliente | Settore | Sede | Dimensione |
|---------|---------|------|------------|
| Sedisp Srl | Logistica / magazzini conto terzi | Buccinasco (MI) | ~€10M |
| Autotrasporti Guerra Graziano Srl | Trasporto merci naz./int. | Pesaro | ~€20M, 100+ dip. |
| DN Logistica Srl | Intermodale + logistica integrata | Catania | ~€42M, 100-199 dip. |
| Truck One Srl | Autotrasporti | Marche | PMI |
| Gugel Srl | Trasporto mobili/arredo | Sernaglia d. Battaglia (TV) | ~€35M, 230 dip. |
| Autotrasporti De Girolami SpA | Trasporto arredo alta gamma | Motta di Livenza (TV) | ~€32M, 171 dip. |
| Comeco Srl | Logistica avanzata | Pordenone | ~€8,7M |
| Cippà Trasporti SA | Spedizioni + dogana | Chiasso (CH) | 80+ dip. |

**Pattern comune (ICP):**
- Autotrasporto, logistica conto terzi, spedizioni/dogana — spesso a gestione familiare
- Fatturato €5–50M, 20–250 dipendenti
- Italia (con cluster Nord-Est e hub logistici) + Ticino/CH per il cross-border
- **Pain:** volumi alti di fatture vettori/fornitori, CMR, DDT, bolle doganali → data entry manuale in amministrazione. Fit perfetto per OCR AI + estrazione dati fatture.

**Buyer personas:** Responsabile amministrativo / CFO (pain owner) · Titolare/AD (decisore) · Responsabile IT/operations (influencer).

---

## 2. Risultati

- **Universo Apollo:** ~1.150 aziende (NAICS 484/4885/493, IT+CH, 21-500 dip.) + ~3.000 (tag trasporti/spedizioni). Estratte e deduplicate: 190 → curate a mano: **85 lead qualificati**.
- **Tier A — 29 aziende** best-fit (mix dimensione/settore identico ai seed, con lookalike diretti: Laghezza e AMT ≈ Cippà su dogana; Vercesi, Trasporti Romagna, Caloni ≈ Guerra Graziano; Foppiani, Zaninoni ≈ Gugel/De Girolami)
- **Tier B — 56 aziende** in target da qualificare (autotrasporti/spedizioni PMI)
- **38 contatti decision-maker** (CFO, resp. amministrazione, AD/CEO, DG) nelle Tier A

**File dati:** [`data/lookalike-companies.csv`](data/lookalike-companies.csv) · [`data/lookalike-contacts.csv`](data/lookalike-contacts.csv)

### Tier A (top 15 per fatturato)

| Azienda | Dominio | Fatturato | Perché |
|---------|---------|-----------|--------|
| Trasporti Romagna SpA | trasportiromagna.com | €197M | Grande ma pure-player trasporti; CFO+resp. amm. individuati |
| Avion Company SpA | avioninternational.com | €73M | Spedizioni internazionali |
| Mitsafetrans | mitsafetrans.it | €67M | Trasporti & logistica hi-tech |
| Express Global | expressglobal.com | €59M | Spedizioni |
| Laghezza SpA | laghezza.com | €56M | Dogana + logistica ≈ Cippà; resp. amm. individuato |
| Aldieri SpA | aldieri.it | €44M | Trasporti |
| Albatrans Int. Freight Forwarding | albatrans.com | €39M | Freight forwarding; CFO individuato |
| Autotrasporti Vercesi SpA | autotrasportivercesi.com | €34M | Gemello di Guerra Graziano |
| OneExpress Italia SpA | oneexpress.it | €5,5M | Network pallet — alto volume fatture vettori |
| TLC Transportation & Logistic (CH) | tlc-com.ch | €5,5M | Ticino ≈ Cippà; Group CFO individuato |
| Nicoli Trasporti Spedizioni SpA | nicolitrasporta.it | n.d. | Resp. Amministrazione Finanza individuata |
| CST Logistica Trasporti | csttrasporti.it | n.d. | CFO + resp. amm. + resp. operativo individuati |
| Fischer & Rechsteiner SpA | ferfreight.com | n.d. | Spedizioni storiche |
| Ala Trasporti SA (CH) | alatrasporti.ch | n.d. | Ticino ≈ Cippà; GM + admin manager individuati |
| AMT SA (CH) | amt-sa.com | n.d. | CH; CEO + CFO individuati |

Lista completa (29 Tier A + 56 Tier B) nel CSV.

### Contatti chiave (estratto)

| Nome | Ruolo | Azienda |
|------|-------|---------|
| Francesca *** | CFO | CST Logistica Trasporti |
| Veronica *** | Resp. Amministrazione Finanza | Nicoli Trasporti Spedizioni |
| Bruno *** / Linda *** | CFO / Group CFO | Trasporti Romagna |
| Luciana *** | Administrative Manager | Laghezza SpA |
| Andrea *** | CEO | Vector SpA |
| Elvezio *** | CEO | Trasporti Pesanti Srl |
| Fabien *** | Group CFO | TLC (CH) |
| Ruggero *** | Administrative Manager | Girelli Logistics Group |

⚠️ Cognomi ed email mascherati dal piano Apollo: servono ~38 crediti di enrichment (`people_match`) per sbloccarli.

---

## 3. Angolo di outreach suggerito

Hook per il settore: *"Quante fatture vettori/fornitori processa la vostra amministrazione ogni mese? I nostri clienti nel trasporto (aziende come le vostre, 50-200 dipendenti) hanno tagliato il 70-80% del tempo di data entry con estrazione AI di fatture, CMR e DDT — senza cambiare gestionale."*

- **Tier A:** outreach 1:1 personalizzato (email + LinkedIn), leva sui casi seed omologhi (es. a Laghezza si cita il caso "spedizioniere doganale").
- **Tier B:** sequenza semi-automatica dopo qualificazione rapida (sito + fatturato).

## 4. Prossimi step

1. **Enrichment contatti** (email verificate): ~38 crediti Apollo su approvazione.
2. Seconda passata people-search sui domini Tier B (gratuita) per completare i contatti.
3. Import in sequenza Apollo / CRM e avvio outreach Tier A.
4. Le ricerche hanno altre ~4.000 aziende disponibili nelle pagine successive (1 credito/pagina) se serve volume.

---

*Crediti Apollo consumati in questa run: 2 (ricerche aziende). People search: gratuita.*
