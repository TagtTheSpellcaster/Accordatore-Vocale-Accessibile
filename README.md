# Accordatore Vocale Accessibile

[![Version](https://img.shields.io/badge/version-1.1.0-blue.svg)](https://github.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![PWA Ready](https://img.shields.io/badge/PWA-Ready-success.svg)](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps)
[![Web Audio API](https://img.shields.io/badge/Web_Audio_API-Supported-orange.svg)](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API)

Un'applicazione web progressiva (PWA) progettata per permettere a persone non vedenti o ipovedenti di accordare strumenti musicali (arpa, chitarra, ukulele, basso) in totale autonomia, combinando sintesi vocale automatica, gesti touch accessibili e un gauge dinamico a 60 FPS.

## Caratteristiche Principali

* **Selezione Strumenti via Gesti (v1.1.0):** Con uno swipe orizzontale a destra o sinistra si seleziona la modalità desiderata con annuncio vocale immediato:
  * **Cromatico** (tutte le 12 note)
  * **Chitarra** (con indicazione del numero della corda da 1 a 6)
  * **Ukulele** (con indicazione del numero della corda da 1 a 4)
  * **Basso** (con indicazione del numero della corda da 1 a 4)

* **Sintesi Vocale Intelligente (Web Speech API):** Pronuncia automaticamente il nome della nota/corda e lo stato dell'intonazione (*"accordato"*, *"troppo alto"*, *"troppo basso"*) non appena il suono si stabilizza.

* **Prevenzione Auto-Ascolto (Mute Flag):** Disattiva temporaneamente l'ascolto del microfono durante la pronuncia vocale per evitare che lo smartphone entri in loop ascoltando il proprio altoparlante.

* **Gauge Visivo Rettangolare ad Alto Contrasto:**
  * Sfumatura continua da rosso (calante/crescente) a verde (centro perfetto).
  * Movimento fluido dell'ago basato su **interpolazione lineare (LERP)** e smorzamento del rumore (*Passa-Basso*).

* **Interfaccia Tattile Touch a Schermo Intero:** L'intero schermo funziona come superficie touch per avviare l'ascolto, cambiare strumento o richiedere a voce l'ultimo stato rilevato.

* **100% Progressive Web App (PWA):** Installabile su iOS, Android, Windows e Mac. Funziona totalmente offline tramite Service Worker.

## Installazione e Uso

### Utilizzo via Browser o PWA

1. Apri la Web App tramite il link fornito da GitHub Pages (es. `https://<tuo-utente>.github.io/<nome-repo>/`).
2. **Installazione su Smartphone:**
   * **Android (Chrome):** Tocca il menu a tre pallini e seleziona **"Aggiungi a schermata Home"** o **"Installa app"**.
   * **iOS (Safari):** Tocca l'icona di condivisione e seleziona **"Aggiungi alla schermata Home"**.
3. **Comandi rapidi:**
   * **Tocco singolo:** Avvia l'accordatore o rilegge a voce l'ultimo stato rilevato.
   * **Swipe Destra / Sinistra (o Frecce tastiera):** Scambia la modalità tra Cromatico, Chitarra, Ukulele e Basso.

## Struttura del Progetto

```
.
├── index.html        # Struttura HTML, CSS ad alto contrasto e logica JS (v1.1.0)
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