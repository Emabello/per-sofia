# per-sofia

Pagina anniversario. Un solo file: `index.html`. Niente build, niente librerie, niente CDN.

## Pronta

Il form è già collegato a Formspree (`https://formspree.io/f/mgaedyqk`), in cima allo `<script>`:

```js
const FORM_ENDPOINT = "https://formspree.io/f/mgaedyqk";
```

**Prima di mandarle il link, fai un invio di prova tu.** Formspree, la primissima volta,
può chiedere una conferma via mail: se non l'hai ancora fatta, il primo invio vero
potrebbe non arrivare. Meglio scoprirlo adesso che l'11.

Se svuoti la costante, la pagina torna in modalità prova: il flusso funziona ma la mail
non parte, e in fondo compare un avviso che lo dice.

A Sofia non viene mai chiesta la sua mail: arriva tutto a te.

## Metterla online

**GitHub Pages** — Settings → Pages → Source: `Deploy from a branch`, branch `main`, cartella `/ (root)`.
Dopo un minuto è su `https://emabello.github.io/per-sofia/`.

**Netlify Drop** — trascina `index.html` su [app.netlify.com/drop](https://app.netlify.com/drop).

## Le cinque scene

1. **Apertura** — "Sofia, apri qui". Il primo tocco sblocca audio e animazioni su iOS.
2. **Contatore** — i giorni insieme, count-up che rallenta verso la fine.
3. **La lettera** — busta che si apre, vibrazione breve, testo riga per riga. Qui i petali si diradano.
4. **I quattro tile** — ognuno con le sue domande (vedi sotto).
5. **Chiusura** — conferma, countdown ai quattro anni e il gattino.

## I quattro tile

Ognuno ha intro, etichette e domande sue. Si cambiano tutti nell'oggetto `OPZIONI` nel JS.

| Tile | Chiede |
|---|---|
| Una serata fuori | Che fame abbiamo? · Pizza / Sushi / Qualcosa di carino / Scegli tu |
| Un appuntamento con me | Quanto tempo ho? · Un paio d'ore / Tutto il pomeriggio / Fino a sera / Decidi tu |
| Un viaggio | Quanto stiamo fuori? + Che aria tira? (due domande) |
| Sorprendimi tu | Quanto posso esagerare? · Poco / Il giusto / Esagera / Fai tu |

Cambiano anche le etichette dei picker ("Che sera", "Si parte il", "Ti passo a prendere alle")
e il suggerimento nel campo libero. Le risposte finiscono nella mail con la domanda per esteso:

```json
{
  "scelta": "Un viaggio",
  "giorno": "16/10/2026",
  "ora": "09:30",
  "messaggio": "ma non troppo lontano",
  "Quanto stiamo fuori?": "Un weekend",
  "Che aria tira?": "Montagna"
}
```

Le chip sono facoltative: se non ne tocca nessuna arriva `(non detto)`, non si blocca niente.

## Il gattino

Ce ne sono due. Uno **di sfondo**, piccolo, che scappa dal dito o dal mouse dalla scena 2 in poi
e resta sempre fuori dal blocco di testo (se non ha spazio, sparisce).

Uno **grande alla fine**, sotto il countdown, in mezzo ai petali che cadono:
i primi due tocchi scappa ("eh no", "quasi"), al terzo si arrende e fa le fusa — occhi
felici, respiro, vibrazione e un suono di fusa generato al momento. Da lì in poi
continua a fare le fusa a ogni tocco.

## Cosa è calcolato da solo

Niente numeri scritti a mano. Tutto parte da:

```js
const DATA_INIZIO = "2022-10-11";
```

Da lì escono i giorni insieme, il "tre anni e undici mesi" (anche dentro la lettera) e il
countdown finale. L'11/09/2026 dice **1431 giorni** e **"tre anni e undici mesi"**;
il giorno dopo si aggiorna da solo, plurali compresi.

## Note

- Musica generata con la Web Audio API: nessun file, nessun copyright, parte al primo tocco.
- Se il browser blocca l'audio, il tastino mute sparisce e il resto funziona uguale.
- Le scene avanzano solo al tocco. Mai un timer.
- Rispetta `prefers-reduced-motion`.
- Petali solo via `transform`/`opacity`: 24 su mobile, 33 nella scena finale.
- Testata a 320, 375, 414px e su desktop.
