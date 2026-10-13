# Brief condiviso — Landing Page "Life Saver" by Digital Bear

Questo è il documento di contesto comune a tutti gli agenti della pipeline.
Ogni agente legge questo brief e produce SOLO il proprio output nella cartella indicata.

## Obiettivo
Landing page commerciale, a pagina singola, per **Life Saver**: la piattaforma di sicurezza
di Digital Bear che collega dispositivo IoT, rete cellulare, piattaforma cloud, dashboard e App
smartphone, riutilizzata su più use case (oggi **Smart Bike** e **Smart Ski**, domani altri).
Tono: accattivante e concreto, non troppo complessa, ma con sostanza tecnica credibile.
Lingua: **italiano**.

## Pubblico
1. Decisori business (outdoor, sport, rental, comprensori sciistici, assicurazioni, enti).
2. Referenti tecnici che vogliono capire "come funziona davvero".

## Messaggio chiave
"Quando succede qualcosa, ogni secondo conta. Life Saver rileva, localizza e allerta — anche dove lo smartphone non arriva."

## Componenti reali della soluzione (fonte: prototipo fotografato, `assets/device-prototype.jpg`)
- Modulo cellulare **SIMCom SIM7080G** → LTE-M / **NB-IoT** (copertura profonda, bassi consumi).
- Ricevitore GNSS **Quectel L86** (antenna patch integrata, multi-costellazione).
- Sensore inerziale (accelerometro/IMU) per rilevare cadute e urti.
- Display TFT a colori: ID dispositivo (es. `SB_XXXXX` = Smart Bike), tempo sessione,
  livello segnale cellulare, stato fix satellitare, tecnologia radio e qualità (es. "LTE NB-IOT · RSRP −93 · RSRQ −11").
- Pulsanti fisici (SOS / funzione), buzzer, LED di stato, slot microSD (log locale), USB-C (alimentazione/ricarica).
- Già realizzati: **App smartphone**, **dispositivo IoT**, **piattaforma IoT**, **dashboard** per use case.

## Flusso operativo (da rappresentare)
1. **Rileva** — IMU rileva caduta/urto anomalo, oppure l'utente preme SOS.
2. **Localizza** — fix GNSS, posizione + contesto (velocità, ultimo movimento).
3. **Trasmetti** — evento via NB-IoT/LTE-M alla piattaforma (non dipende dallo smartphone).
4. **Elabora** — la piattaforma valida l'evento, applica regole per use case, apre un incidente.
5. **Allerta** — notifiche a App, contatti di emergenza, centrale operativa/dashboard.
6. **Intervieni** — mappa live, storico, chiusura incidente.

## Vincoli di onestà (IMPORTANTI)
- NON inventare clienti, testimonianze, loghi partner, certificazioni, premi o numeri di mercato.
- Numeri ammessi solo se tecnici e generici/qualitativi (es. "NB-IoT", "multi-costellazione GNSS").
  Se serve un valore non noto, usare un segnaposto evidente tipo `[DA CONFERMARE]`.
- Contatti: email segnaposto `info@digitalbear.example` — da sostituire.

## Identità visiva
- Tema scuro "tecnico" ispirato al display del device: sfondo blu notte (#0B1220), accenti
  verde lime (#B8F04A, come i testi del display), azzurro (#4CC3FF), rosso allarme (#FF4D4D), ambra (#FFC247).
- Font: "Space Grotesk" (titoli) + "Inter" (testo) + "JetBrains Mono" (dettagli tecnici), da Google Fonts.
- Stile icone/illustrazioni: line-art SVG, tratto 1.5–2px, angoli arrotondati.
- Mobile-first, nessuno scroll orizzontale, gutter 16px su mobile.

## Struttura pagina (sezioni)
1. Hero (headline, sottotitolo, 2 CTA, visual del device con display animato)
2. Il problema (3 scenari: ciclista caduto in zona isolata, sciatore fuori pista, telefono scarico/senza campo)
3. Come funziona (flusso 6 step)
4. Architettura end-to-end (diagramma Device → Rete → Piattaforma → Dashboard/App)
5. Il dispositivo (foto prototipo reale + callout componenti)
6. Una piattaforma, tanti use case (Smart Bike, Smart Ski, + "prossimi": lavoratori isolati, escursionismo, flotte)
7. Dashboard & App (mockup)
8. Specifiche tecniche (tabella sintetica)
9. CTA finale (richiedi demo / pilota)
10. Footer

## Output degli agenti
- `agentic/10-copy.md` — Agente Copywriter
- `assets/svg/*.svg` — Agente Visual
- `index.html` — Integratore (assemblaggio)
- `agentic/30-qa.md` — Agente QA
