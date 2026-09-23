# Lead Qualifier — skill configurabile

Skill per Claude che qualifica un lead B2B partendo da dominio + pagina LinkedIn company. Il metodo (fetch live, scoring solo su dati osservabili, zero dati inventati, messaggio di primo contatto) è fisso; offerta, ICP, settori, soglie, ruoli e stile dei messaggi sono tuoi e stanno in `config.yaml`.

## File

| File | Cosa contiene |
|---|---|
| `SKILL.md` | Il motore: fasi, regole di scoring, formato output. Non va modificato per adattarlo. |
| `config.example.yaml` | Schema della configurazione, vuoto e commentato. |
| `config.yaml` | La tua configurazione (non versionata: vedi `.gitignore`). |

## Setup

**Opzione A — configurazione guidata**
1. Carica la cartella senza `config.yaml` (su claude.ai: Impostazioni → Capabilities → Skills → carica lo zip della cartella).
2. Scrivi "configura la skill lead-qualifier". Claude fa 12 domande in 3 blocchi e restituisce il `config.yaml`.
3. Salva il file nella cartella della skill come `config.yaml` e ricarica lo zip, oppure caricalo nei file del progetto come `lead-qualifier-config.yaml`.

**Opzione B — manuale**
1. Copia `config.example.yaml` in `config.yaml` e compila.
2. Zippa la cartella e caricala.

## Uso

"Qualifica acme.com — linkedin.com/company/acme"

## Regole che la config non può scavalcare

- Nessun numero senza fonte.
- Dimensione senza dato verificato = esclusa dalla media, non stimata.
- Note interne (prezzi, ACV) mai nel messaggio al prospect.
- Clienti riservati mai nominati.
