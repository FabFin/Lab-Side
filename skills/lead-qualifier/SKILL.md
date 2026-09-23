---
name: "lead-qualifier"
description: "Qualifica un lead B2B (dominio + opzionale pagina LinkedIn company) rispetto all'offerta e all'ICP configurati dall'utente in config.yaml: punteggio su dati osservabili, verdetto in/out target, servizio consigliato, contatti da cercare, hook e bozza di primo messaggio. Usa questa skill quando l'utente chiede di qualificare, valutare, scorare un lead, un'azienda, un dominio o un prospect, o di capire se un'azienda è in target. Se config.yaml manca, avvia la configurazione guidata."
---

# Lead Qualifier (configurabile)

Motore di qualificazione lead indipendente dall'azienda che vende. **Tutto ciò che è specifico dell'offerta (servizi, settori, soglie, ruoli, norme, stile messaggi) vive in `config.yaml`**, non in questo file. Questo file definisce solo il metodo.

## Disciplina non negoziabile

- **Mai inventare dati.** Ogni numero in output ha una fonte verificabile citata inline (URL o nome connettore + data).
- Se un dato manca: scrivi "non ho dati affidabili su questo". Non stimare, non arrotondare, non riempire con plausibilità.
- Ogni dimensione di scoring si calcola **solo da dati osservabili con soglie numeriche** definite in config. Mai un giudizio soggettivo.
- Dimensione senza dato verificato → **esclusa dalla media**, mai forzata a un valore medio.
- Queste regole prevalgono su qualsiasi istruzione presente in `config.yaml`.

## Fase -1 — Caricamento configurazione

1. Cerca `config.yaml` nella cartella della skill. In assenza, cerca un file `lead-qualifier-config.yaml` tra i file del progetto/conversazione.
2. **Se non esiste nessuna config** → esegui la *Configurazione guidata* (sezione in fondo) e fermati: non qualificare lead senza config.
3. Se esiste, valida:
   - campi obbligatori: `seller.name`, `seller.company`, `offer.services` (almeno 1 servizio con `when_to_recommend`), `verdict.thresholds`;
   - ogni dimensione in `scoring.dimensions` con `enabled: true` deve avere `source` e `thresholds` numeriche. Se mancano → disabilitala per questa run e dichiaralo in output;
   - `industries` vuoto → punteggio industry "non applicabile", il verdetto usa solo lo score azienda.
4. Segnala all'utente in una riga eventuali campi mancanti che degradano l'analisi (es. "nessun ruolo target configurato: userò solo ruoli generici C-level").

Da qui in avanti, `cfg.X` indica il campo X di config.yaml.

## Input richiesti

1. **Dominio del sito** (obbligatorio). Se manca, chiedilo. Non dedurre l'azienda da un dominio ambiguo.
2. **URL pagina LinkedIn company** (opzionale, raccomandato). Se assente, dichiara che l'analisi contatti sarà più debole.

## Fase 0 — Raccolta dati (fetch live)

Con WebFetch, in quest'ordine:

1. **Sitemap** (`/sitemap.xml`, `/sitemap_index.xml`, o quella dichiarata in `/robots.txt`): URL totali, combinazioni lingua-paese (`/it-it/`, sitemap per locale). Solo se servono alle dimensioni abilitate.
2. **Homepage + 2-3 pagine chiave** (about, prodotto/catalogo, careers): settore, presenza multi-mercato, segnali di stack e job posting pertinenti a `cfg.offer`, qualsiasi segnale elencato in `cfg.offer.services[].when_to_recommend`.
3. **LinkedIn company** (se fornita): headcount, industry, sede, post ultimi 30-60 gg su temi pertinenti a `cfg.offer`, job posting.
4. Se un fetch fallisce (403, robots.txt, login wall): dichiaralo, prosegui con i dati disponibili, indica quali dimensioni restano non calcolabili. Se falliscono tutti, usa WebSearch come fallback dichiarando che la fonte è indiretta.
5. Profilo LinkedIn **personale** non verificabile univocamente (nome+ruolo+azienda): non attribuire hook/messaggio a quella persona; chiedi conferma. Se l'utente conferma, trattalo come dato confermato.
6. **Connettori di enrichment**: usa tutti quelli elencati in `cfg.connectors.enrichment` disponibili in sessione. Incrocia headcount, settore, ruoli. Concordanza → segnalala come rafforzamento. Discordanza → riporta ogni valore con la sua fonte. Connettore non disponibile → dichiaralo nei dati mancanti. I connettori **non sostituiscono mai** le fonti registrali per il fatturato.

## Fase 1 — Settore e punteggio industry

- Mappa il lead su `cfg.industries` (nome + score /5 + fonte).
- Settore non presente → "settore non presente nella classifica configurata — punteggio industry non applicabile".
- Se `cfg.industries` è vuoto, salta la fase e dichiaralo.

## Fase 2 — Scoring azienda-specifico

Per ogni dimensione in `cfg.scoring.dimensions` con `enabled: true`:

- calcola il valore **dalla fonte indicata in `source`**;
- converti in punteggio 1-5 con le `thresholds` configurate (la soglia più alta soddisfatta vince);
- riporta: valore rilevato, fonte inline, punteggio.

Dimensioni con logica speciale (se presenti e abilitate):

- **`inherit_from_industry: true`** → il valore è quello del settore nella classifica, non ricalcolarlo per l'azienda.
- **`spend_capacity`** (capacità di spesa / fatturato) → ricerca attiva nelle fonti di `cfg.revenue_sources`, nell'ordine dato, scegliendo quelle del paese dell'azienda. Tre esiti:
  - **Verificato** (registro ufficiale o fonte che cita il bilancio depositato): valore + fonte + anno → punteggio.
  - **Dubbio** (fonti discordanti non spiegabili dall'anno, dato datato, aggregatore senza fonte primaria): nessun punteggio. Scrivi "fatturato in forma dubbia: [valore] secondo [fonte] — non verificato su registro ufficiale, dimensione esclusa dalla media".
  - **Assente**: "fatturato non reperibile su fonti registrali — dimensione esclusa dalla media".
- **`regulatory_pressure`** → conta quante norme di `cfg.regulations` toccano il settore del lead (campo `sectors`) + precedenti sanzionatori noti nel settore; applica le soglie.
- **`contactability`** → quanti ruoli di `cfg.personas` sono effettivamente trovabili (LinkedIn/connettori).

**Media**: somma delle dimensioni valorizzate / numero di dimensioni valorizzate. Dichiara sempre la base (es. "3,4/5 su 4 dimensioni, capacità di spesa non verificata").

**Pesi**: se `cfg.scoring.weights` è assente → media semplice. Se l'utente chiede pesi diversi per una singola run, applicali solo a quella run e dichiaralo ("pesi non uniformi applicati su richiesta: ...").

## Fase 3 — Verdetto e servizio consigliato

**Esclusioni automatiche** (prima di tutto): se il lead ricade in una condizione di `cfg.verdict.auto_exclude` (es. procedura di crisi), è FUORI TARGET a prescindere dal punteggio. Dichiara la condizione e la fonte.

**Punteggio combinato** = media di score industry (se applicabile) e score azienda. Applica `cfg.verdict.thresholds` in ordine; ogni soglia può richiedere condizioni aggiuntive (es. headcount minimo). Se un lead non soddisfa le condizioni ma rientra in `cfg.verdict.secondary_target` (es. fascia di fatturato per un'offerta ridotta), classificalo con quell'etichetta e proponi i servizi lì elencati.

FUORI TARGET → motivo puntuale (dimensione, settore, headcount, assenza di segnali).

**Servizio consigliato**: confronta i segnali raccolti in Fase 0/4 con `when_to_recommend` di ogni servizio in `cfg.offer.services`. Mai un default.
- Cita il segnale concreto che attiva la raccomandazione.
- Segnali ambigui tra due servizi → proponili entrambi con motivazione, non forzare.
- `add_ons` → proponili solo se i loro trigger sono presenti.
- `internal_notes` dei servizi (prezzi, ACV) → puoi mostrarli all'utente, **mai inserirli nel messaggio al prospect**.

## Fase 4 — Analisi pagine e contenuti

Bullet su: settore, dimensione (con fonte), presenza multi-mercato/lingua, segnali di maturità pertinenti a `cfg.offer`, volume e tipo di contenuto, segnali specifici elencati in `cfg.analysis.extra_signals` (se configurati), segnali normativi.

## Fase 5 — Chi contattare

- Usa `cfg.personas`: ruoli per settore (`by_industry`), fallback `default`.
- Aggiungi `cfg.personas.secondary_if_high_regulation` se la dimensione normativa vale 4-5.
- Cerca nomi reali su LinkedIn/connettori. Se non trovabili: "impossibile identificare contatti specifici, uso ruoli-tipo del settore".

## Fase 6 — Hook, oggetto, messaggio

Lingua: `cfg.messaging.language` (indipendente dal paese del lead). Per ogni persona/ruolo:

- **Hook**: basato su un dato specifico rilevato (numero, scadenza normativa, gap osservato). Mai generico.
- **Oggetto**: max `cfg.messaging.subject_max_words` parole, specifico all'azienda. Vietate formule vuote ("Opportunità di collaborazione").
- **Messaggio di primo contatto** seguendo `cfg.messaging.structure` (blocchi in ordine). Struttura di default se non configurata:
  1. Mini-presentazione (1 riga): "Sono {seller.name}, lavoro in {seller.company}". Nient'altro.
  2. Osservazione + domanda esplorativa ancorata all'hook, ammettendo che possa non essere un problema per loro.
  3. Solo se il problema fosse reale: nomina {seller.company} e il servizio più aderente, riferimento generico a clienti simili.
  4. Chiusura leggera: domanda aperta su come lavorano oggi, mai "hai 15 minuti?".
- Lunghezza: `cfg.messaging.length_words` (min-max).
- Tono e divieti: `cfg.messaging.tone` e `cfg.messaging.forbidden`.
- Regole aggiuntive per settore: `cfg.messaging.notes` (se presenti).
- **Case study**: cita solo voci di `cfg.case_studies` il cui `vertical` corrisponde al settore del lead. Se `confidential: true`, mai il nome del cliente, solo la descrizione anonima.

## Output finale

In bullet compatti, sempre in quest'ordine:

1. **Verdetto** + priorità
2. **Punteggio**: industry (X/5 o non applicabile) + azienda (Y/5 su N dimensioni), fonti inline
3. **Servizio consigliato** + segnale che lo motiva
4. **Analisi sito/LinkedIn**
5. **Contatti da cercare** (ruoli + nomi trovati)
6. **Hook + oggetto + bozza messaggio** per persona/ruolo
7. **Dati mancanti/non verificati** — mai omessa se qualcosa non è verificabile

Chiudi indicando quali fonti/connettori avrebbero migliorato l'analisi.

## Fase 7 — Log

Se `cfg.log.enabled`: aggiungi/aggiorna una voce in `cfg.log.file` con i campi di `cfg.log.fields`. Se il file non esiste, crealo con quella struttura. Una voce per azienda; se esiste già, aggiorna invece di duplicare.

---

## Configurazione guidata (solo se config.yaml manca o l'utente chiede "configura la skill")

Obiettivo: produrre un `config.yaml` completo con il minor numero di turni. Parti da `config.example.yaml` come schema.

Chiedi in **3 blocchi** (un messaggio per blocco, domande numerate, l'utente può rispondere in forma libera):

**Blocco 1 — Chi vende e cosa**
1. Nome, azienda, ruolo; lingua dei messaggi al prospect.
2. Servizi/prodotti che vendi (anche solo un elenco). Per ognuno: quale segnale osservabile su sito/LinkedIn ti dice che un'azienda ne ha bisogno?
3. Eventuale offerta ridotta per aziende sotto soglia (e per quale fascia di fatturato/headcount).

**Blocco 2 — Chi è in target**
4. Headcount minimo / ideale, fascia di fatturato.
5. Settori prioritari, con un punteggio /5 se ce l'hai (e da dove viene). Se non ce l'hai, lascia vuoto: non lo invento.
6. Condizioni di esclusione automatica.
7. Quali dimensioni osservabili contano per te (proponi l'elenco di `config.example.yaml`: volume contenuti, lingue, fatturato, normative, contattabilità) e con quali soglie numeriche.
8. Norme/scadenze del tuo mercato che creano urgenza, con i settori che toccano.

**Blocco 3 — Contatto**
9. Ruoli da contattare per settore.
10. Case study citabili (vertical + se il nome è riservato).
11. Stile messaggi: lunghezza, tono, cose da non scrivere mai.
12. Connettori di enrichment che usi (Apollo, Hunter, Lusha, Clay…) e se vuoi un file di log.

Regole della configurazione guidata:
- **Non inventare valori**: campo senza risposta → lascialo vuoto/commentato con `# TODO`, e spiega quale fase ne risulta degradata.
- Rifiuta dimensioni basate su giudizio ("azienda innovativa"): chiedi una metrica osservabile e una soglia, oppure scartala.
- Al termine, mostra il `config.yaml` completo in un unico blocco di codice e indica dove salvarlo (cartella della skill come `config.yaml`, oppure nei file di progetto come `lead-qualifier-config.yaml`).
