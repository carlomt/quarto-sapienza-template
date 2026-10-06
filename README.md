# Quarto Sapienza Template

Un modello Quarto Revealjs per presentazioni.

Fondo bianco, titoli leggeri, testo grigio, accenti bordeaux e copertina con logo Sapienza. Formato 16:9, senza animazioni. Il tema usa font di sistema e non richiede font remoti.

## Inizia una nuova presentazione

1. Crea un repository con **Use this template → Create a new repository**, oppure copia questa cartella.
2. Apri `slides.qmd` e modifica i dati iniziali: titolo, autore, email, evento e data.
3. Sostituisci le slide di esempio. Duplica i layout che ti servono.
4. Compila e apri l'anteprima:

```bash
quarto render
quarto preview slides.qmd
```

L'HTML si trova in `_output/slides.html`. Include immagini, stile e librerie, quindi può essere copiato e aperto anche offline.

Requisito: [Quarto](https://quarto.org/docs/get-started/). La versione usata per la compilazione di riferimento e fissata nel workflow è **1.9.37**. Non servono Python, R, Node o LaTeX per le slide di esempio.

## Struttura

```text
_quarto.yml                     Impostazioni condivise della presentazione
slides.qmd                      Metadati, contenuti e note
assets/
  logo-sapienza.png              Logo della copertina
  README.md                     Indicazioni sulle immagini
theme/
  sapienza.scss                 Tema e layout
  slide-numbers.html            Numerazione automatica
.github/workflows/render.yml    Compilazione GitHub Actions
.gitignore                      Esclusione di output e cache
```

Il `.qmd` è un file Markdown con metadati Quarto. È l'unico sorgente dei contenuti: non occorre mantenere una seconda copia `.md`.

## La copertina si modifica in un solo punto

All'inizio di `slides.qmd`:

```yaml
pagetitle: "Titolo della presentazione"
author: "Nome Cognome"
email: "nome@example.org"
event: "Nome del convegno · Città"
event-date: "Giorno mese anno"
lang: it
```

I campi compaiono nella copertina tramite i [metadati Quarto](https://quarto.org/docs/authoring/variables.html). Usa `pagetitle`, non `title`: il titolo della pagina HTML e quello della copertina restano allineati senza generare una seconda copertina automatica.

Per forzare una divisione del titolo su due righe, modifica il blocco `.cover-title` in `slides.qmd` e inserisci `<br>`. In questo caso aggiorna anche `pagetitle` per il titolo della scheda del browser.

Per un altro logo, cambia il percorso dell'immagine della copertina. Il logo Sapienza incluso è quello della presentazione originale, mantenuto nelle proporzioni originali.

## Layout disponibili

| Classe | Uso |
|---|---|
| `.cover` | Copertina con logo, titolo, autore ed evento |
| `.lead` | Frase introduttiva più grande |
| `.columns` e `.column` | Colonne Quarto; lascia il 4% complessivo per lo spazio fra due colonne |
| `.takeaway` | Conclusione bordeaux con una riga sottile |
| `.small` | Nota di contesto |
| `.source` | Fonte o didascalia |
| `.compact-table` | Tabella con spazi ridotti, applicata al titolo della slide |
| `.process` | Tabella di processo con colonne per fase, attività e risultato |
| `.steps` | Lista numerata più compatta, applicata al titolo della slide |
| `.side-image` | Immagine in una colonna |
| `.figure-wide` | Figura a tutta larghezza |
| `.wide-chart` | Grafico ampio con maggiore altezza |
| `.plot-subtitle` | Sottotitolo di una figura |
| `.closing-lead` e `.closing-contact` | Conclusione e contatti |
| `.backup` | Slide di riserva con numerazione B1, B2, … |
| `.unnumbered` | Slide senza numero e fuori dal conteggio |
| `.references` | Elenco di riferimenti |

Il segnaposto `.figure-placeholder` mostra dove inserire una figura. Sostituiscilo, ad esempio, con:

```markdown
![Descrizione del grafico](assets/figura.svg){.side-image}
```

Mantieni la dimensione della presentazione a 1600 × 900: il tema usa posizioni definite per questo formato e Quarto lo adatta allo schermo. Per cambiare rapporto d'aspetto occorre adattare anche il tema.

## Numerazione e note

Le slide principali iniziano da **1**, escludendo copertina e slide `.unnumbered`. Le slide `.backup` hanno un conteggio separato **B1, B2, …**. Puoi aggiungere, eliminare e riordinare slide senza cambiare soglie nel codice.

Esempio:

```markdown
## Dettagli del metodo {.backup}

- Approfondimento per le domande.

::: notes
Spiegazione riservata al relatore.
:::
```

Le note sono invisibili al pubblico, ma sono incluse nel sorgente dell'HTML condiviso. Le durate nelle note sono indicazioni per la prova dell'intervento, non un avanzamento automatico.

Scorciatoie: frecce o spazio per avanzare, `F` per lo schermo intero, `S` per la vista relatore, `Esc` per la panoramica. La vista relatore funziona meglio tramite `quarto preview`; il browser può chiedere di consentire la finestra popup.

## Personalizzare lo stile

In `theme/sapienza.scss` modifica `$accent` per cambiare il colore principale. Le variabili iniziali definiscono font e colori; le regole successive definiscono margini e layout.

Il tema privilegia pochi elementi leggibili. Quando una slide è troppo piena, suddividi il contenuto prima di ridurre il carattere. Conserva assi, unità e legenda dei grafici a dimensioni leggibili.

Per formule LaTeX, sostituisci `html-math-method: plain` in `_quarto.yml` con un motore matematico Quarto e verifica l'HTML risultante. L'esempio iniziale evita dipendenze matematiche esterne.

## GitHub Actions

Il workflow compila le slide a ogni push, pull request o avvio manuale. Nella pagina della run trovi l'artefatto **slides-html**, conservato per 30 giorni. Gli output compilati non vengono aggiunti alla storia Git.

È una compilazione con artefatto scaricabile. Per avere un URL pubblico della presentazione puoi aggiungere successivamente la pubblicazione con GitHub Pages. [Documentazione Quarto](https://quarto.org/docs/publishing/github-pages.html).

## PDF

Apri l'anteprima, aggiungi `?print-pdf` all'URL prima dell'eventuale `#`, quindi usa la stampa del browser in PDF. Attiva gli sfondi e disattiva intestazioni e piè di pagina del browser. Controlla il risultato prima di distribuirlo.

## Verifica dell'esportazione iniziale

Il modello è stato compilato con Quarto 1.9.37. Sono stati controllati struttura, sostituzione dei metadati, risorse incorporate e logica della numerazione. L'anteprima visiva nel browser e l'esecuzione su GitHub Actions non sono state effettuate in questa sessione.
