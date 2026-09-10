# per-sofia

Pagina anniversario. Un solo file: `index.html`. Niente build, niente librerie, niente CDN.

## Prima di mandarle il link — 1 cosa sola

Apri `index.html`, cerca in cima allo `<script>`:

```js
const FORM_ENDPOINT = "";
```

1. Vai su [formspree.io](https://formspree.io), crea un form, verifica la tua mail.
2. Copia l'URL che ti danno (`https://formspree.io/f/xxxxxxx`) e incollalo lì dentro.

Finché è vuoto la pagina va in **modalità prova**: il flusso funziona tutto ma la mail
non parte, e in fondo compare un avviso scuro che lo dice. L'avviso sparisce da solo
appena incolli l'URL.

> Funziona con qualsiasi endpoint che accetti un POST JSON, non solo Formspree.
> Il JSON che invia è: `scelta`, `dettaglio`, `giorno`, `ora`, `messaggio`, `_subject`.

A Sofia non viene mai chiesta la sua mail: la mail arriva a te dal servizio.

## Metterla online

**GitHub Pages** — Settings → Pages → Source: `Deploy from a branch`, branch `main`, cartella `/ (root)`.
Dopo un minuto è su `https://emabello.github.io/per-sofia/`.

**Netlify Drop** — trascina `index.html` su [app.netlify.com/drop](https://app.netlify.com/drop).

## Cosa è calcolato da solo

Niente numeri scritti a mano. Tutto parte da:

```js
const DATA_INIZIO = "2022-10-11";
```

Da lì escono i giorni insieme, il "tre anni e undici mesi" (anche nella lettera) e
il countdown finale ai quattro anni. L'11/09/2026 dice **1431 giorni** e
**"tre anni e undici mesi"**; il giorno dopo si aggiorna da solo.

## Note

- Musica generata con la Web Audio API: nessun file audio, nessun copyright, parte al primo tocco.
- Se il browser blocca l'audio, il tastino mute sparisce e il resto funziona uguale.
- Le scene avanzano solo al tocco. Mai un timer.
- Rispetta `prefers-reduced-motion`.
- Testata a 320, 375 e 414px e su desktop.
