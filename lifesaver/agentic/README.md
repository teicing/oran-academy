# Pipeline agentica — Landing Page Life Saver

La landing page è stata costruita da una piccola squadra di agenti coordinati da un orchestratore.
Ogni agente ha un ruolo, un input e un output precisi; il brief condiviso evita che lavorino su ipotesi diverse.

```
                 ┌──────────────────────┐
                 │  00-brief.md         │  Orchestratore: obiettivo, pubblico,
                 │  (contesto comune)   │  componenti reali, vincoli di onestà
                 └─────────┬────────────┘
                           │
            ┌──────────────┴──────────────┐        (in parallelo)
            ▼                             ▼
┌───────────────────────┐     ┌───────────────────────┐
│ Agente Copywriter     │     │ Agente Visual         │
│ → 10-copy.md          │     │ → assets/svg/*.svg    │
│ testi per sezione     │     │ device, flussi,       │
│                       │     │ architettura, mockup  │
└───────────┬───────────┘     └───────────┬───────────┘
            └──────────────┬──────────────┘
                           ▼
              ┌────────────────────────┐
              │ Integratore            │
              │ → index.html           │  layout responsive, animazioni,
              └───────────┬────────────┘  assemblaggio testi + grafica
                          ▼
              ┌────────────────────────┐
              │ Agente QA              │  screenshot desktop/mobile,
              │ → 30-qa.md             │  overflow, contrasto, link,
              └───────────┬────────────┘  coerenza col brief
                          ▼
                    fix finali → commit
```

## Ruoli

| Agente | Input | Output | Criterio di "fatto" |
|---|---|---|---|
| Orchestratore | richiesta, foto prototipo | `00-brief.md` | sezioni, palette, vincoli definiti |
| Copywriter | brief | `10-copy.md` | tutte le 10 sezioni, nessun dato inventato |
| Visual | brief + foto | `assets/svg/` | SVG validi, renderizzati e ricontrollati |
| Integratore | copy + SVG | `index.html` | pagina singola, mobile-first, zero build |
| QA | pagina | `30-qa.md` | nessun overflow, link ok, `[DA CONFERMARE]` elencati |

## Come rieseguirla per un nuovo use case
1. Aggiorna `00-brief.md` (es. aggiungi "Smart Worker" nella sezione use case).
2. Rilancia Copywriter e Visual sulle sole sezioni interessate.
3. L'integratore sostituisce i blocchi corrispondenti in `index.html`.
4. QA ripete i controlli.

## Vincoli permanenti
- Niente clienti, testimonianze, certificazioni o statistiche inventate.
- I valori non noti restano marcati `[DA CONFERMARE]` finché non vengono validati.

## Iterazione v2 — riposizionamento B2B2C · NB-NTN · multitenant
- Input aggiuntivo: design "EU-LS Architect Solution" (`ref/eu-ls-architecture.png`) e nuova strategia del cliente.
- `01-brief-v2.md`: messaggi chiave, roadmap breve/medio/lungo termine, struttura reale della piattaforma
  (edge Californium + Scandium, CoAP DTLS Gateway, core ThingsBoard CE + PostgreSQL, NBI) ed esempio di payload calcolato.
- Agente Visual v2 → `platform.svg`, `coap-ack.svg`, `payload-compare.svg`, `roadmap.svg`, `b2b2c.svg`, `ntn-coverage.svg`.
- Integratore → nuove sezioni in `index.html`: NB-NTN, B2B2C, Piattaforma, CoAP Gateway, Roadmap; aggiornati hero, specifiche e CTA.
- I testi v2 sono scritti direttamente in `index.html`; `10-copy.md` resta come storico della v1.

## Iterazione v3
- Rinominata la soluzione in **EU-LS · European Life Saver** e corretto il modulo in **SIMCom SIM7070G HP-S** (NB-NTN).
