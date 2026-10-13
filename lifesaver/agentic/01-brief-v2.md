# Brief v2 — Riposizionamento Life Saver (B2B2C · NB-NTN · Piattaforma multitenant)

Integra `00-brief.md` (palette, font, vincoli di onestà restano validi).
Riferimento architetturale fornito dal cliente: `agentic/ref/eu-ls-architecture.png` ("EU-LS Architect Solution").

## Messaggi chiave (in ordine di importanza)
1. **Modello B2B2C**: Digital Bear → Partner B2B (comprensori sciistici, noleggi bike/e-bike,
   assicurazioni, operatori/telco, organizzazioni outdoor, aziende con lavoratori isolati) → Utente finale (C).
   Il partner usa la piattaforma con il proprio tenant, brand, regole e dashboard.
2. **Punto di forza oggi: dispositivo NB-NTN capable** — NB-IoT terrestre + **NB-NTN satellitare**
   (3GPP Rel-17, satellite GEO a ~37.000 km, banda S). Dove non c'è copertura terrestre, il messaggio passa via satellite.
3. **Piattaforma multitenant** — il vero asset che resta nel tempo.
4. **Roadmap & spostamento del valore**:
   - Breve termine: Device (NB-IoT terrestre + NB-NTN) + Smartphone (LTE/NR) → Piattaforma IoT + Dashboard.
   - Medio termine: Device (NB-IoT + NB-NTN) + Smartphone (LTE/NR) + primi Smartphone NTN-capable (LTE/NR + NTN) → Piattaforma.
   - Lungo termine: Smartphone (LTE/NR + NTN + 6G) → Piattaforma.
   - Valore: Device 70% + Piattaforma 30% → Piattaforma 100%.
   - Motivo: roadmap 3GPP degli smartphone NTN, deployment massivo; attrito iniziale = costo aggiuntivo del
     collegamento satellitare oltre a quello terrestre. Nel lungo periodo lo smartphone sostituisce il device.
   - Beneficio: si eliminano i costi dell'asset hardware (logistica, riparazione HW, sostituzioni, batterie).
   - La piattaforma sarà già funzionante e integrata con smartphone LTE/NR e poi NTN.
5. **La vera struttura della piattaforma** (dal design):
   - Device → rete MNO + SMO, senza nominare l'operatore (eNodeB banda B20 terrestre, oppure GEO S-band via NTN) → CN-NSA → **UDP 5684**
   - **EDGE: Eclipse Californium + Scandium** — Anti-DDoS · Rate Limit · Load Balancer · **CoAP DTLS Gateway**
     (DTLS termination PSK / X.509 · anti-replay / session cache · payload validation JSON/CBOR ·
     device identity mapping · rate limiting per device · stateless, horizontal scaling N+1)
   - → **HTTP REST / MQTT** →
   - **CORE: ThingsBoard CE + PostgreSQL** — Data Collection · Data Storage · Data Exposure
     (Device Registry · Telemetry ingestion · Rule Engine · Dashboards)
   - → **NBI** (Northbound Interface) → **REST APIs** → Customer / Partner.
   - Stack device→edge: CoAP / DTLS / UDP. Payload: CBOR (o JSON).
6. **Perché il CoAP Gateway conta**:
   - Riduce drasticamente il payload: CBOR binario + header CoAP di 4 byte, niente handshake TCP/TLS per messaggio.
   - Rende affidabile un trasporto connection-less: messaggi CoAP **Confirmable (CON)** → **ACK** dalla
     piattaforma (piggybacked, con codice di risposta, es. 2.04 Changed), Message-ID per deduplica, ritrasmissione
     con backoff esponenziale se l'ACK non arriva.
   - Su GEO la latenza di andata e ritorno è nell'ordine del mezzo secondo: i timer di ritrasmissione si adattano.

## Esempio di payload (calcolato, da usare nei grafici)
Evento: `{"id":"SB_00412","ev":"FALL","lat":45.07049,"lon":7.68682,"spd":18.4,"bat":78,"ts":1760371200}`
- JSON compatto: **94 byte**
- CBOR con chiavi testuali: **74 byte**
- CBOR con chiavi intere (schema compatto): **52 byte** (≈ −45%)

Stima indicativa per un singolo evento su IPv4 (etichettare SEMPRE "stima indicativa"):
- HTTPS (HTTP/1.1 + TLS 1.3 + TCP): payload 94 + header HTTP ~150 + TLS ~22 + TCP 20 + IP 20 ≈ **~306 byte**,
  più handshake TCP (3 pacchetti) e TLS a ogni nuova connessione, più ACK TCP.
- CoAP/DTLS (CON + CBOR): payload 52 + CoAP ~12 + DTLS 1.2 (CCM_8) ~29 + UDP 8 + IP 20 ≈ **~121 byte**,
  sessione DTLS riutilizzata, 1 ACK CoAP con esito applicativo.

## Onestà
- Il prototipo fotografato monta SIMCom SIM7080G (NB-IoT / LTE-M). Il modulo NB-NTN va indicato come
  "[DA CONFERMARE]" — non attribuire NB-NTN al SIM7080G.
- Percentuali 70/30 → 100: sono la visione strategica del cliente, presentarle come "distribuzione del valore (visione)".
- Nessuna data precisa per le fasi: usare "Oggi / Prossimi anni / Lungo periodo" o "Breve / Medio / Lungo termine".
