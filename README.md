# Accordatore Vocale Accessibile

Un'applicazione web progressiva (PWA) progettata per permettere a persone non vedenti o ipovedenti di accordare strumenti musicali (come l'arpa o la chitarra) in totale autonomia, combinando sintesi vocale automatica, alto contrasto visivo e un gauge dinamico a 60 FPS.

## Caratteristiche Principali

* **Sintesi Vocale Intelligente (Web Speech API):** Pronuncia automaticamente il nome della nota e lo stato dell'intonazione (*"accordato"*, *"troppo alto"*, *"troppo basso"*) non appena il suono si stabilizza.

* **Prevenzione Auto-Ascolto (Mute Flag):** Disattiva temporaneamente l'ascolto del microfono durante la pronuncia vocale per evitare che lo smartphone entri in loop ascoltando il proprio altoparlante.

* **Gauge Visivo Rettangolare ad Alto Contrasto:**

  * Sfumatura continua da rosso (calante/crescente) a verde (centro perfetto).

  * Indicatori spessi e visibili pensati per ipovedenti.

  * Movimento fluido dell'ago basato su **interpolazione lineare (LERP)** e smorzamento del rumore (*Passa-Basso*).

* **Interfaccia Tattile Touch a Schermo Intero:** L'intero schermo funziona come un unico grande pulsante per avviare l'accordatore o richiedere a voce l'ultimo stato rilevato.

* **100% Progressive Web App (PWA):** Installabile su iOS, Android, Windows e Mac. Funziona totalmente offline tramite Service Worker.

## Installazione e Uso

### Utilizzo via Browser o PWA

1. Apri la Web App tramite il link fornito da GitHub Pages (es. `https://<tuo-utente>.github.io/<nome-repo>/`).

2. **Installazione su Smartphone:**

   * **Android (Chrome):** Tocca il menu a tre pallini e seleziona **"Aggiungi a schermata Home"** o **"Installa app"**.

   * **iOS (Safari):** Tocca l'icona di condivisione e seleziona **"Aggiungi alla schermata Home"**.

3. **Primo avvio:** Tocca in un punto qualsiasi dello schermo per concedere i permessi del microfono e avviare l'ascolto.

## Struttura del Progetto

```
.
├── index.html        # Struttura HTML, CSS ad alto contrasto e logica JS
├── manifest.json     # Descrittore per l'installazione PWA
├── sw.js             # Service Worker per la gestione della cache offline
├── icon-192.png      # Icona applicazione (192x192)
└── icon-512.png      # Icona applicazione (512x512)

```

## Dettagli Tecnici

* **Pitch Detection:** Rilevamento della frequenza fondamentale ($F_0$) tramite algoritmo di **Autocorrelazione** su campioni di dati nel dominio del tempo tramite `AudioContext` e `AnalyserNode`.

* **Risoluzione Cents:** Calcolo logaritmico degli scostamenti in cents rispetto allo standard di intonazione $A_4 = 440\text{ Hz}$:
  

  $$
  \text{cents} = 1200 \times \log_2\left(\frac{f}{f_{\text{target}}}\right)
  $$

* **Decoupling Grafico/Voce:** La resa visiva del gauge aggiorna la posizione a 60 FPS slegata dalla coda di messaggi vocali per mantenere l'interfaccia ultra-reattiva.

## Licenza

Distribuito sotto licenza **MIT**. Consulta il file `LICENSE` per maggiori informazioni.