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
| Una serata fuori | Che fame abbiamo? · Pizza / Sushi / Qualcosa di carino / Scegli tu — più "Un posto in mente?" |
| Un appuntamento con me | Quanto tempo ho? · Un paio d'ore / Tutto il pomeriggio / Fino a sera / Decidi tu — più "Da dove ti passo a prendere?" |
| Un viaggio | Quanto stiamo fuori? + Che aria tira? — più "Dove ti va di andare?" con 22 mete suggerite |
| Sorprendimi tu | Quanto posso esagerare? · Poco / Il giusto / Esagera / Fai tu |

### Il posto — tarato su Milano

- **Serata** e **appuntamento**: 22 zone di Milano suggerite (Navigli, Brera, Isola, NoLo,
  Porta Romana, Ticinese, Paolo Sarpi…). Può anche scrivere il nome del locale.
- **Viaggio**: 28 mete da weekend raggiungibili da Milano (i laghi, Bergamo Alta,
  Franciacorta, Portofino, le Cinque Terre, Bormio, Courmayeur, Verona, Bologna…).

Il campo resta comunque libero: la lista è un suggerimento, non una gabbia.

Appena scrive qualcosa compare **"cercalo su Maps ↗"**, che apre la ricerca già pronta in una
scheda nuova, con "Milano" aggiunto dove serve. Non è l'API di Google Maps — quella vorrebbe
una chiave e chiamate esterne, e questa pagina non ha dipendenze. È solo un link, ma fa lo
stesso lavoro: lei guarda, sceglie, e scrive il nome nel campo.

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

## Il gattino e il suo gioco

Uno **di sfondo**, piccolo, che scappa dal dito o dal mouse dalla scena 2 in poi e resta
sempre fuori dal blocco di testo (se non ha spazio, sparisce).

Alla fine, accanto al pulsante **"clicca qui per il gattino"**, ce n'è uno disegnato per bene:
soriano rosso a strisce, con pupille che seguono quello che guarda, palpebre che sbattono,
orecchie che si drizzano, coda che ondeggia e zampine che si alternano quando cammina.

Il pulsante apre un **pop-up trasparente**: niente sfocatura, così lo sfondo e i petali si
vedono uguali attraverso il pannello, e altri petali cadono anche davanti. Il testo della
scena 5 si nasconde finché il gioco è aperto.

Il gattino gira **dentro e fuori il riquadro** — ogni tanto se ne va a spasso sopra o sotto il
pannello. Se finisce sopra i comandi diventa trasparente ai tocchi, così i pulsanti restano
sempre premibili.

Quattro giochi, più le coccole:

| Gioco | Cosa fa |
|---|---|
| **Puntatore** | il pallino rosso segue il dito, lui lo insegue e ci salta sopra |
| **Gomitolo** | tocchi dove tirarlo, lui lo raggiunge e lo scaraventa via |
| **Piuma** | la muovi, lui la azzanna e quella scappa |
| **Crocchette** | metti la ciotola, lui ci arriva e mangia (con rumore di crocchette) |
| **Coccola** | tocchi lui: occhi felici, cuoricini, fusa e vibrazione |

Ogni cosa riempie la barra **fusa**. A 100 parte la festa: pioggia di cuoricini, petali
intensificati e "Ti vuole bene, pata."

Tutti i versi (fusa, miagolio, crocchette) sono generati con la Web Audio API. Nessun file.
Si chiude con la X o con Esc, e il fuoco resta dentro il pop-up finché è aperto.

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
- Petali solo via `transform`/`opacity`: 34 su mobile (54 su desktop), +14 nella scena finale,
  +16 nel pop-up del gioco.
- **Rete di sicurezza sui petali**: dopo il contatore la pagina misura i fotogrammi veri per
  un secondo e mezzo. Sopra i 40 fps non tocca niente; sotto, dirada i petali da sola (fino al
  60% in meno). Così su un telefono in forma restano tutti, e su uno stanco la pagina non
  diventa a scatti.

## Test

- **iPhone 13 su WebKit vero** (il motore di Safari, profilo dispositivo ufficiale 390×664):
  26 controlli, tutti passati.
- **Chromium** a 320/375/414/1280 e con `prefers-reduced-motion`: 63 controlli.
- Le richieste a Formspree sono sempre intercettate: nessuna mail di prova spedita davvero.

Quello che **non** si può verificare da qui: la fluidità reale su un iPhone. Questo container
non ha GPU e disegna via software, quindi i numeri di fps non sono confrontabili (una pagina
vuota fa 61 fps, la nostra 20 — su hardware vero quel carico lo fa la GPU senza fatica).
La rete di sicurezza qui sopra esiste proprio per questo.
