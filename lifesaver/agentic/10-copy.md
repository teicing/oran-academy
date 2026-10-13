# 10 — Copy della landing page "Life Saver" by Digital Bear

Autore: Agente Copywriter · Lingua: italiano · Fonte: `agentic/00-brief.md`

## Note per l'Integratore e il QA

- Rispettati i vincoli di onestà: nessun cliente, testimonianza, logo partner, certificazione, premio o numero di mercato.
- I valori non noti sono marcati `[DA CONFERMARE]`: vanno lasciati visibili finché il team non li conferma.
- I testi in `monospace` sono pensati per il font JetBrains Mono.
- Formulazione prudente sulla copertura: NB-IoT/LTE-M offrono copertura profonda, ma servono comunque rete cellulare e copertura dell'operatore. Non scrivere "funziona ovunque" né "anche senza rete".
- Protocolli: niente MQTT/CoAP dati per certi; si citano solo come esempio.
- Email: `info@digitalbear.example` è un segnaposto da sostituire.

---

## 1. Hero

**Eyebrow:** Piattaforma di sicurezza IoT · by Digital Bear

**Headline, 3 varianti:**

- A ★ **PREFERITA:** Quando succede qualcosa, ogni secondo conta.
- B: Rileva. Localizza. Allerta. Anche quando il telefono tace.
- C: Chi è da solo all'aperto non dovrebbe restarci quando cade.

**Motivo della scelta (A):** riprende parola per parola il messaggio chiave del brief, parla subito sia ai decisori business sia ai tecnici e lascia al sottotitolo il "come".

**Sottotitolo (24 parole):**
Life Saver rileva cadute e richieste di SOS, localizza la persona e allerta chi può intervenire, tramite rete cellulare IoT e senza dipendere dallo smartphone.

**CTA:**

- Primaria: **Richiedi una demo**
- Secondaria: **Guarda come funziona** (ancora a §3)

**Proof chip:**

- `NB-IoT / LTE-M`
- `GNSS multi-costellazione`
- `Rilevamento cadute`

**Testo del display animato (visual del device; valori dimostrativi, coerenti con il prototipo):**

```
SB_XXXXX
SESSIONE 00:42:17
LTE NB-IOT · RSRP −93 · RSRQ −11
GNSS FIX ✓
```

**Microcopy sotto le CTA (facoltativo):** Prototipo funzionante. Progetti pilota aperti.

---

## 2. Il problema

**Eyebrow:** Il problema

**Titolo:** Gli incidenti non scelgono il momento giusto.

**Sottotitolo:** Spesso chi cade è da solo, non riesce a chiamare o non sa dire dove si trova. I minuti persi diventano il vero rischio.

**Scenario 1 · Ciclista in zona isolata**
Una curva su una strada di collina, una caduta, nessuno in giro. Il ciclista è a terra e non riesce a prendere il telefono.

**Scenario 2 · Sciatore fuori pista**
Una deviazione fuori dal tracciato battuto, poi un urto. Nessuno lo ha visto uscire e nessuno sa dove cercarlo.

**Scenario 3 · Telefono scarico o senza campo**
La batteria è finita da un'ora, oppure il segnale va e viene. Proprio quando serve chiamare aiuto, lo smartphone non risponde.

**Frase di chiusura (transizione verso §3):** Life Saver nasce per i momenti in cui la persona non può chiedere aiuto da sola.

---

## 3. Come funziona

**Eyebrow:** Come funziona

**Titolo:** Dall'evento all'intervento, in sei passaggi.

**Sottotitolo:** Il dispositivo agisce da solo e non aspetta lo smartphone. La piattaforma trasforma un segnale in un incidente da gestire.

**Step 1 · Rileva**
Il sensore inerziale riconosce una caduta o un urto anomalo. In alternativa, l'utente preme il pulsante SOS.
`IMU → evento: FALL_DETECTED | SOS_PRESSED`

**Step 2 · Localizza**
Il ricevitore GNSS calcola la posizione. All'evento si aggiungono velocità e ultimo movimento.
`GNSS fix · lat/lon · velocità · timestamp`

**Step 3 · Trasmetti**
L'evento parte sulla rete cellulare IoT verso la piattaforma. Il telefono dell'utente non serve.
`uplink NB-IoT / LTE-M · SIM7080G`

**Step 4 · Elabora**
La piattaforma valida l'evento e applica le regole dello use case. Se le condizioni sono confermate, apre un incidente.
`rules engine · use case: bike | ski → incident OPEN`

**Step 5 · Allerta**
Le notifiche raggiungono App, contatti di emergenza e centrale operativa. Ognuno vede la stessa posizione.
`notify → app · contatti · dashboard`

**Step 6 · Intervieni**
L'operatore segue la mappa live e consulta lo storico. A soccorso completato chiude l'incidente.
`incident: OPEN → IN_CORSO → CHIUSO`

---

## 4. Architettura end-to-end

**Eyebrow:** Architettura

**Titolo:** Un sistema completo, dal sensore allo schermo.

**Sottotitolo:** Quattro livelli già realizzati e integrati tra loro. Ogni livello fa una cosa sola, e la fa in modo affidabile.

**Livello 1 · Device**

- Rileva cadute e urti con il sensore inerziale e gestisce il pulsante SOS.
- Calcola la posizione con il GNSS multi-costellazione.
- Salva un log locale su microSD e mostra lo stato sul display.

**Livello 2 · Rete cellulare**

- Usa NB-IoT e LTE-M, pensate per oggetti connessi a basso consumo.
- Offre copertura profonda anche in zone difficili per lo smartphone.
- Invia pacchetti piccoli e frequenti con un consumo energetico contenuto.

**Livello 3 · Piattaforma IoT**

- Riceve la telemetria tramite protocolli IoT leggeri (ad esempio MQTT o CoAP).
- Valida gli eventi e applica regole specifiche per ogni use case.
- Apre, traccia e archivia gli incidenti con il loro storico completo.

**Livello 4 · Dashboard & App**

- Dashboard web per la centrale operativa: mappa live, incidenti, flotta.
- App smartphone per l'utente e i suoi contatti di emergenza.
- Notifiche in tempo reale verso tutti i soggetti coinvolti.

**Etichette del diagramma (brevi):** `Device` → `Rete NB-IoT / LTE-M` → `Piattaforma IoT` → `Dashboard` + `App`

---

## 5. Il dispositivo

**Eyebrow:** Il dispositivo

**Titolo:** Hardware vero, già sul banco di prova.

**Sottotitolo:** Questo è il prototipo funzionante di Life Saver. Ogni componente ha un compito preciso.

**Didascalia foto:** Prototipo Life Saver, configurazione Smart Bike. Immagine reale, non un rendering.

**Callout componenti:**

1. **Modulo cellulare SIMCom SIM7080G** — Si connette in NB-IoT e LTE-M, consumando poco.
2. **GNSS Quectel L86** — Antenna integrata e più costellazioni per una posizione affidabile.
3. **Sensore inerziale (IMU)** — Riconosce cadute e urti anche se l'utente non reagisce.
4. **Display TFT a colori** — Mostra ID, sessione, segnale e fix satellitare a colpo d'occhio.
5. **Pulsante SOS** — Un gesto fisico per chiedere aiuto, anche con i guanti.
6. **Buzzer e LED di stato** — Confermano l'invio dell'allarme e segnalano lo stato del dispositivo.
7. **Slot microSD** — Registra un log locale degli eventi, utile per analisi successive.
8. **USB-C** — Alimentazione e ricarica con un connettore standard.

Nota: il callout 5 dice "anche con i guanti". Va verificato sul prototipo; se non è confermato, sostituire con "Un gesto fisico e immediato per chiedere aiuto."

---

## 6. Una piattaforma, tanti use case

**Eyebrow:** Use case

**Titolo:** Una piattaforma, tanti scenari.

**Sottotitolo:** Dispositivo, rete e piattaforma restano gli stessi. Per ogni use case cambiano regole, dashboard ed esperienza utente.

### Smart Bike · ATTIVO

**Badge:** Attivo · ID dispositivo `SB_XXXXX`

- Rilevamento di cadute e urti su strada, sterrato e percorsi in quota.
- Invio della posizione GNSS anche lontano dai centri abitati.
- Tracciamento della sessione: durata, percorso, ultimo movimento noto.
- Adatto a ciclisti privati, flotte e-bike e noleggi.

### Smart Ski · ATTIVO

**Badge:** Attivo

- Rilevamento di cadute e urti in pista e fuori pista.
- Posizione dello sciatore inviata alla centrale del comprensorio.
- SOS manuale con un pulsante fisico, facile da premere anche con i guanti.
- Regole dedicate al contesto neve, gestite dalla piattaforma.

Nota obbligatoria (piccola, sotto la card Smart Ski): Life Saver non è un ARTVA e non sostituisce i dispositivi di ricerca in valanga.

### Prossimi use case · IN ARRIVO

- **Lavoratori isolati** — Protezione per chi opera da solo in cantieri, impianti o zone remote.
- **Escursionismo e trekking** — Un allarme che parte anche quando il sentiero si fa isolato.
- **Flotte e noleggio** — Sicurezza dell'utente e visibilità sui mezzi in un'unica dashboard.

**Microcopy:** Hai un altro scenario? Parliamone.

---

## 7. Dashboard & App

**Eyebrow:** Dashboard & App

**Titolo:** Tutti vedono la stessa situazione, in tempo reale.

**Sottotitolo:** La centrale operativa ha il quadro completo. L'utente e i suoi contatti sanno cosa sta succedendo.

### Dashboard (centrale operativa)

1. **Mappa live** — Mostra dispositivi e incidenti aperti con la loro posizione aggiornata.
2. **Gestione incidenti** — Raccoglie stato, priorità e note in un'unica vista, dall'apertura alla chiusura.
3. **Storico ed eventi** — Permette di ricostruire percorsi, allarmi e interventi passati.
4. **Stato dei dispositivi** — Segnale cellulare, fix GNSS e ultima comunicazione per ogni device.

### App smartphone

1. **Allarmi in tempo reale** — Una notifica appena la piattaforma apre un incidente.
2. **Contatti di emergenza** — Scegli chi avvisare e come.
3. **Sessione e percorso** — Per seguire l'attività in corso e rivedere quelle passate.
4. **Stato del dispositivo** — Mostra connessione, posizione e controlli a portata di mano.

**Etichetta mockup:** Interfacce reali in sviluppo. Le schermate sono illustrative.

---

## 8. Specifiche tecniche

**Eyebrow:** Specifiche

**Titolo:** Le specifiche, senza giri di parole.

**Sottotitolo:** Riepilogo del prototipo attuale. Alcuni valori sono ancora in fase di validazione.

| Voce | Specifica |
|---|---|
| Connettività | Cellulare LTE-M / NB-IoT · modulo SIMCom SIM7080G |
| GNSS | Quectel L86 · multi-costellazione · antenna patch integrata |
| Sensori | Sensore inerziale (accelerometro / IMU) per cadute e urti |
| Interfaccia | Display TFT a colori · pulsanti fisici (SOS / funzione) |
| Allarmi | Automatici (caduta/urto) e manuali (SOS) · buzzer e LED di stato |
| Storage | Slot microSD per log locale |
| Alimentazione | USB-C (alimentazione e ricarica) · batteria [DA CONFERMARE] |
| Autonomia | [DA CONFERMARE] |
| Grado di protezione | [DA CONFERMARE] |
| Piattaforma | Piattaforma IoT cloud · dashboard web · App smartphone |

**Nota sotto la tabella:** Specifiche riferite al prototipo. Possono cambiare nella versione di produzione.

---

## 9. CTA finale

**Eyebrow:** Iniziamo

**Titolo:** Portiamo Life Saver sul tuo territorio.

**Sottotitolo:** Gestisci un comprensorio, un servizio di noleggio, una flotta o un'organizzazione outdoor? Costruiamo insieme un progetto pilota sul tuo use case.

**CTA:**

- Primaria: **Richiedi una demo**
- Secondaria: **Proponi un progetto pilota**

**Microcopy:** Scrivici a `info@digitalbear.example`. Ti rispondiamo con una proposta concreta.

---

## 10. Footer

**Tagline:** Life Saver by Digital Bear: rileva, localizza, allerta.

**Colonne link:**

| Prodotto | Use case | Azienda | Contatti |
|---|---|---|---|
| Come funziona | Smart Bike | Digital Bear | info@digitalbear.example |
| Architettura | Smart Ski | Progetti pilota | Richiedi una demo |
| Il dispositivo | Prossimi use case | | |
| Specifiche | | | |

**Riga legale:** © 2026 Digital Bear. Tutti i diritti riservati. · Privacy [DA CONFERMARE] · Cookie [DA CONFERMARE]
